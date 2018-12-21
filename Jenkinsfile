@Library('github.com/fabric8io/osio-pipeline@pod_template') _
def utils = new io.openshift.Utils()

osio {
  
  config runtime: 'java', version: '1.8'

  ci {
     integrationTestCmd = "mvn verify integration-test -Dnamespace.use.current=false -Dnamespace.use.existing=${utils.usersNamespace()} -Dit.test=*IT -DfailIfNoTests=false -DenableImageStreamDetection=true -Popenshift,openshift-it"
     runTest commands: integrationTestCmd
  }

  cd {

    def resources = processTemplate(params: [
          release_version: "1.0.${env.BUILD_NUMBER}"
    ])
    echo "CD build"

    build resources: resources
    deploy resources: resources, env: 'stage'
    deploy resources: resources, env: 'run', approval: 'manual'

  }
}
