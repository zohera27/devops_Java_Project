@Library('Jenkins_Shared_Library') _

pipeline{
    
    agent any

    parameters{
        
        choice(name: 'action', choices: 'create\ndelete', description: 'Choose Create/Destroy')
    }

    stages{

        

        stage('Git Checkout') {

         when { expression { params.action == 'create' } }

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

         when { expression { params.action == 'create' } }
        
            steps{

                script{

                    mvnTest()
                }
            }
        }

        stage('Integration Test maven') {

         when { expression { params.action == 'create' } }

            steps{

                script{

                    mvnIntegrationTest()
                }
            }
        }        

        stage('Static Code Analysis: Sonarqube') {

         when { expression { params.action == 'create' } }

            steps{

                script{

                    statiCodeAnalysis()
                }
            }
        } 

    }
}