pipeline{
    agent any

        stages{
              stage('Git Checkout'){
                steps{
                     script{
                        git 'https://github.com/ChethanGowda6464/demo-counter-app.git'
                           }
                    }
         }
         stage('Unit Testing'){
                steps{
                     script{
                        sh 'mvn test'
                           }
                    }
         }
         stage('Intigration Testing'){
                steps{
                     script{
                        sh 'mvn verify -DskipUnitTests'
                           }
                    }
         }
          stage('Maven Build'){
                steps{
                     script{
                        sh 'mvn clean install'
                           }
                    }
         }
         stage('static code analysis'){
                steps{
                     script{
                        withSonarQubeEnv(credentialsId: 'sonar-id') {
                              sh 'mvn clean package sonar:sonar'
                             }
                           }
                    }
         }
          stage('Quality gate status'){
                steps{
                     script{
                        waitForQualityGate abortPipeline: false, credentialsId: 'sonar-id'
                          }
                    }
         }
     }
}