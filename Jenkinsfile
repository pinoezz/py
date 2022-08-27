node{
   try{
      def registry = "registry.digitalocean.com/oca-docr/my-python-app"
      def k8s_config_dev = "do-sgp1-test-cluster"
      def deploy_dev = "my-python-app"

      stage('Pull Repository') {
         git branch: 'staging', credentialsId: '58684a41-0049-4cf8-b8b5-83077b6b505d', url: 'git@github.com:pinoezz/py.git'
      }

         }
      }  
      stage('Build') {
         sh "DOCKER_BUILDKIT=1 docker build -t ${registry}:dev-${BUILD_NUMBER} ."
      }
      stage('Push') {
         sh "docker push ${registry}:dev-${BUILD_NUMBER}"
      }
      stage('Set k8s-context') {
         sh "kubectl config use-context ${k8s_config_dev}"
  }
