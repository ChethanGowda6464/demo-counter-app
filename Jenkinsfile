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
     }
}