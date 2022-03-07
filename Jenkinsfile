pipeline {
    agent any

    stages {
        stage("clone code"){
            steps{
                git url: 'https://github.com/praneethss/addressbook.git'
            }
        }
        stage('Build') {
            steps{
                sh "mvn clean install package"
            }
        }
        stage('sonar'){
            steps{
                withSonarQubeEnv(installationName: 'Sonar', credentialsId: 'Sonar_Cred'){
                sh "mvn sonar:sonar"
                }
            }
        }
        stage('Deploy'){
            steps{
                deploy adapters: [tomcat8(credentialsId: 'Tomcat_Cred', path: '', url: 'http://ec2-3-86-205-4.compute-1.amazonaws.com:8090/')], contextPath: null, war: '**/*.war'
            }
        }
    }
}
