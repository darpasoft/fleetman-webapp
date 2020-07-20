node {
    stage('Preparation') { 
        git 'https://github.com/darpasoft/fleetman-webapp'
    }
    stage('Build') {
        sh "mvn clean package"
   }
    stage('Results') {
        junit '**/target/surefire-reports/TEST-*.xml'
        archiveArtifacts 'target/*.war'
    }
    stage('deploy') {
        withCredentials([[$class: 'AmazonWebServicesCredentialsBinding', accessKeyVariable: 'AWS_ACCESS_KEY_ID', credentialsId: 'aws_credentials_2', secretKeyVariable: 'AWS_SECRET_ACCESS_KEY']]) {
            ansiblePlaybook credentialsId: 'ssh-cred', installation: 'ansible-installation', playbook: 'deploy.yaml'
        }   
    }
}
