@Library('Jenkins_Shared_Library') _

pipeline{
    
    agent any

    parameters{
        
        choice(name: 'action', choices: 'create\ndelete', description: 'Choose Create/Destroy')
        String(name: 'ImageName', description: "Name of the Docker Build", defaultValue: 'javapp')
        String(name: 'ImageTag', description: "Tag of the Docker Build", defaultValue: 'v1')
        String(name: 'AppName', description: "Name of the Application", defaultValue: 'springboot')
    
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

                    def SonarQubecredentialId = 'sonar-api'
                    statiCodeAnalysis(SonarQubecredentialId)
                }
            }
        }

        stage('Quality Gate Satus Check: Sonarqube') {

         when { expression { params.action == 'create' } }

            steps{

                script{

                    def SonarQubecredentialId = 'sonar-api'
                    QualityGateStatus(SonarQubecredentialId)
                }
            }
        }

        stage('Maven Build : maven') {

         when { expression { params.action == 'create' } }
        
            steps{

                script{

                    mvnBuild()
                }
            }
        }

        stage('Docker Image Build') {

         when { expression { params.action == 'create' } }
        
            steps{

                script{

                    dockerBuild("${params.ImageName}", "${params.ImageTag}", "${params.AppName}")
                }
            }
        }

    }
}