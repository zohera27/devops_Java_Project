@Library('Jenkins_Shared_Library') _

pipeline{
    
    agent any

    parameters{
        
        choice(name: 'action', choices: 'create\ndelete', description: 'Choose Create/Destroy')
    }

    stages{

        when { expression { param.action == 'create' } }

        stage('Git Checkout') {

            steps{

                script{

                    gitCheckout(
                        branch: "main",
                        url: "https://github.com/zohera27/devops_Java_Project.git"
                    )
                }
            }
        }

        stage('Unit Test maven') {

         when { expression { param.action == 'create' } }
        
            steps{

                script{

                    mvnTest()
                }
            }
        }

        stage('Integration Test maven') {

         when { expression { param.action == 'create' } }

            steps{

                script{

                    mvnIntegrationTest()
                }
            }
        }        

        stage('Static Code Analysis: Sonarqube') {

         when { expression { param.action == 'create' } }

            steps{

                script{

                    statiCodeAnalysis()
                }
            }
        } 

    }
}