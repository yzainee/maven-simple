@Library('github.com/fabric8io/osio-pipeline@pod_template') _
def utils = new io.openshift.Utils()

osio {
  
  config runtime: 'java', version: '1.8'

  ci {

    def app = processTemplate(params: [
          RELEASE_VERSION: "1.0.${env.BUILD_NUMBER}"
    ])
    echo "CI Build"
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
