node{
   try{
      def registry = "registry.digitalocean.com/oca-docr/my-python-app"
      def k8s_config_dev = "do-sgp1-test-cluster"
      def deploy_dev = "my-python-app"

      stage('Pull Repository') {
         git branch: 'staging', credentialsId: '58684a41-0049-4cf8-b8b5-83077b6b505d', url: 'git@gitlab.com:sample-python.git'
      }
      stage('Code Quality') { 
         script {
         def scannerHome = tool 'sonarqube-dev';
             withSonarQubeEnv("sonarqube-dev") {
             sh "${tool("sonarqube-dev")}/bin/sonar-scanner \
             -Dsonar.projectKey=sms-new-scheduler-dev \
             -Dsonar.sources=. \
             -Dsonar.host.url=https://sonarqube.ocatelkom.co.id \
             -Dsonar.login=006274e1606631f47733a97953bc71a2f460fd60"
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
