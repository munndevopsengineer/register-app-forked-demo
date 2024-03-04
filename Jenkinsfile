pipeline {
    agent { label 'Jenkins-Agent' }
    tools {
        jdk 'Java17'
        maven 'Maven3'
    }
    stages{
        stage("Cleaning Up the Jenkins Workspace"){
                steps {
                cleanWs()
                }
        }

        stage("Checkout from SCM"){
                steps {
                    git branch: 'main', credentialsId: 'github', url: 'https://github.com/munndevopsengineer/register-app-forked-demo'
                }
        }

        stage("Build Application"){
            steps {
                sh "mvn clean package"
            }

       }f

       stage("Test Application"){
           steps {
                 sh "mvn test"
           }
       }

   //     stage("SonarQube Analysis"){
   //         steps {
	  //          script {
		 //        withSonarQubeEnv(credentialsId: 'jenkins_sonarqube_token') 
			// { 
   //                      sh "mvn sonar:sonar"
		 //        }
	  //          }	
   //         }
   //     }

   //     stage("Quality Gate"){
   //         steps {
   //             script {
   //                  waitForQualityGate abortPipeline: false, credentialsId: 'jenkins_sonarqube_token'
   //              }	
   //          }

   //      }
   //  }

}
