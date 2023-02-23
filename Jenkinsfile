pipeline {
    agent any
    
    tools {
        maven "Maven3"
    }

    stages {
        stage('Checkoout') {
            steps {
                checkout scmGit(branches: [[name: '*/main']], extensions: [], userRemoteConfigs: [[credentialsId: 'e01db610-54f8-4d91-9b62-2f09bf22a816', url: 'https://github.com/k-chandureddy/CoachDevops.git']])
            }
        }
        
        stage ("Build") {
            steps {
                sh "mvn clean install -f MyWebApp/pom.xml"
            }
        }
        stage ("dev deploy") {
            steps{
                deploy adapters: [tomcat9(credentialsId: '5ecba445-25fe-4ed7-bf36-9d15cec78cd3', path: '', url: 'http://ec2-18-188-253-180.us-east-2.compute.amazonaws.com:8080/')], contextPath: null, war: '**/*.war'
            }
        }
    }
}
