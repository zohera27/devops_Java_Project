@Library('Jenkins_Shared_Library') _

pipeline{
    
    agent any

    stages{

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

            steps{

                script{

                    mvnTest()
                }
            }
        }

        stage('Integration Test maven') {

            steps{

                script{

                    mvnIntegrationTest()
                }
            }
        }        
        
    }
}