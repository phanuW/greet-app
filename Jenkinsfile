pipeline {
    agent { label 'Jenkins-Agent' }
    tools {
        jdk 'Java17' // name of tools that we added in Jenkins
        maven 'Maven3' // name of tools that we added in Jenkins
    }
    stages{
        stage("Cleanup Workspace"){
                steps {
                cleanWs()
                }
        }

        stage("Checkout from SCM"){
                steps {
                    git branch: 'main', credentialsId: 'github', url: 'https://github.com/phanuW/greet-app'
                }
        }

        stage("Build Application"){
            steps {
                sh "mvn clean package"
            }

       }

       stage("Test Application"){
           steps {
                 sh "mvn test"
           }
       }

       stage("SonarQube Analysis"){
          steps {
           script {
                withSonarQubeEnv(credentialsId: 'jenkins-sonarqube-token') {
                   sh "mvn sonar:sonar"
                }
            }
          }
      }
    }
}
