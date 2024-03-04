pipeline {
    agent { label 'Jenkins-Agent' }
    tools {
        jdk 'Java17'
        maven 'Maven3'
    }
    stages {
        stage ('Cleaning Up the Jenkins Workspace') {
                steps {
                cleanWs()
                }
        }

        stage ('Checkout from SCM') {
                steps {
                    git branch: 'main', credentialsId: 'github', url: 'https://github.com/munndevopsengineer/register-app-forked-demo'
                }
        }

        stage ('Build Application') {
            steps {
                sh 'mvn clean package'
            }
        }

        stage ('Test Application') {
            steps {
                sh 'mvn test'
            }
        }
        
        stage ('Sonarqube Analysis..') {
            steps {
                script {
                     withSonarQubeEnv(credentialsId: 'jenkins-sonarqube-token') {
                     sh "mvn sonar:sonar"
                   } 
                } 
            }
        }

        stage ('Quality gate..') {
            steps {
                script {
                     waitForQualityGate abortPipeline: false, credentialsId: 'jenkins-sonarqube-token' 
                   } 
                } 
            }
        }
    }
}
