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
         stage('upload war file to nexus'){
                steps{
                  
                     script{
//def readPomVersion = readMavenPom file: 'pom.xml'
                       // def nexusRepo = readMavenPom.version.endsWith("SNAPSHOT") ? "demoapp-snapshot" : "demoapp-release"
                       // nexusArtifactUploader artifacts: [[artifactId: 'springboot', classifier: '', file: 'target/Uber.jar', type: 'jar']], credentialsId: 'nexus-id', groupId: 'com.example', nexusUrl: '54.205.230.49:8081', nexusVersion: 'nexus3', protocol: 'http', repository: nexusRepo, version: "${readPomVersion.version}"
                       nexusArtifactUploader artifacts: [[artifactId: 'springboot', classifier: '', file: 'target/Uber', type: 'jar']], credentialsId: 'nexusapp-id', groupId: 'com.example', nexusUrl: '54.160.249.218:8081', nexusVersion: 'nexus3', protocol: 'http', repository: 'demoapplication-release', version: '2.2.2'
                          }
                    }
         }
     }
}