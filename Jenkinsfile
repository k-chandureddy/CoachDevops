pipeline {
    agent any
    
    tools {
        maven "Maven3"
    }

    stages {
        stage('Checkoout') {
            steps {
                checkout([$class: 'GitSCM', branches: [[name: '*/main']], extensions: [], userRemoteConfigs: [[credentialsId: '39a0281c-5ab6-4158-bb33-b7b1aab87117', url: 'https://github.com/akannan1087/myApr2022weekendRepo']]])
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
