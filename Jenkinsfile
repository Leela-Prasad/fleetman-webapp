node {
   stage('Preparation') { 
      git 'https://github.com/Leela-Prasad/fleetman-webapp'
   }
   stage('Build') {
        sh "mvn clean package"
   }
   stage('Results') {
      junit '**/target/surefire-reports/TEST-*.xml'
      archive 'target/*.war'
   }
   stage('Deploy') {
      withCredentials([[$class: 'AmazonWebServicesCredentialsBinding', accessKeyVariable: 'AWS_ACCESS_KEY_ID', credentialsId: 'AWS Credentials', secretKeyVariable: 'AWS_SECRET_ACCESS_KEY']]) {
        ansiblePlaybook credentialsId: 'SSH-Credentails', playbook: 'deploy.yaml' 
      }
   }
}
