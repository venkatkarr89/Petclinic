@Library('my-shared-library') _

pipeline{

    agent any

    parameters{

        choice(name: 'action', choices: 'create\ndelete', description: 'Choose create/Destroy')
        
    }

    stages{

        stage('Git Checkout'){
                    when { expression {  params.action == 'create' } }
            steps{
            gitCheckout(
                branch: "main",
                url: "https://github.com/venkatkarr89/Petclinic.git"
            )
            }
        }
         stage('Unit Test maven'){

         when { expression {  params.action == 'create' } }

            steps{
               script{

                   mvnTest()
               }
            }
        }
         stage('Integration Test maven'){
         when { expression {  params.action == 'create' } }
            steps{
               script{

                   mvnIntegrationTest()
               }
            }
        }
        stage('Static code analysis: Sonarqube'){
         when { expression {  params.action == 'create' } }
            steps{
               script{

                   def SonarQubecredentialsId = 'sonar-api'
                   statiCodeAnalysis(SonarQubecredentialsId)
               }
            }
        }
        stage('Quality Gate Status Check : Sonarqube'){
         when { expression {  params.action == 'create' } }
            steps{
               script{

                   def SonarQubecredentialsId = 'sonar-api'
                   QualityGateStatus(SonarQubecredentialsId)
               }
            }
        }
        stage('Maven Build : maven'){
         when { expression {  params.action == 'create' } }
            steps{
               script{

                   mvnBuild()
               }
            }
        }    
    }
}
