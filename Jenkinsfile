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
        
    }
}