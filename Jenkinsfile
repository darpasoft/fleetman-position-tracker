node {
    stage('Preparation') { 
        git 'https://github.com/darpasoft/fleetman-position-tracker'
    }
    stage('Build') {
        sh "mvn package"
   }
    stage('Results') {
        junit '**/target/surefire-reports/TEST-*.xml'
        archiveArtifacts 'target/*.jar'
    }
    stage('deploy') {
        withCredentials([[$class: 'AmazonWebServicesCredentialsBinding', accessKeyVariable: 'AWS_ACCESS_KEY_ID', credentialsId: 'aws_credentials_2', secretKeyVariable: 'AWS_SECRET_ACCESS_KEY']]) {
            ansiblePlaybook credentialsId: 'ssh-cred', installation: 'ansible-installation', playbook: 'deploy.yaml'
        }   
    }
}
