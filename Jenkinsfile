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
        ansiblePlaybook credentialsId: 'ssh-cred', installation: 'ansible-installation', playbook: 'deploy.yaml'
    }
}
