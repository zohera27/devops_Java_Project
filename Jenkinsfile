@Library('Jenkins_Shared_Library') _

pipeline{
    
    agent any

    environment{

        JAVA8_HOME = "${tool 'JAVA8'}"
        JAVA11_HOME = "${tool 'JAVA11'}"
        MAVEN_HOME = "${tool 'MAVEN'}"
    }

    parameters{
        
        choice(name: 'action', choices: 'create\ndelete', description: 'Choose Create/Destroy')
        string(name: 'ImageName', description: "Name of the Docker Build", defaultValue: 'javapp')
        string(name: 'ImageTag', description: "Tag of the Docker Build", defaultValue: 'v1')
        string(name: 'DockerHubUser', description: "Dokcer HUB User Account", defaultValue: 'zohera27')
        
    }

    stages{
        
        stage('Git Checkout') {

         when { expression { params.action == 'create' } }

            steps{

                script{

                    git.gitcheckout(
                        branch: "main",
                        url: "https://github.com/zohera27/devops_Java_Project.git"
                    )
                }
            }
        }
        /*
        stage('Unit Test maven') {

         when { expression { params.action == 'create' } }
        
            steps{

                script{

                    mvn.mvntest(JAVA8_HOME)
                }
            }
        }

        stage('Integration Test maven') {

         when { expression { params.action == 'create' } }

            steps{

                script{

                    mvn.mvnverify(JAVA8_HOME)
                }
            }
        }  

        stage('Maven Build : maven') {

         when { expression { params.action == 'create' } }
        
            steps{

                script{

                    mvn.mvnbuild(JAVA8_HOME)
                }
            }
        }
        */
        stage('Docker Image Build') {

         when { expression { params.action == 'create' } }
        
            steps{

                script{

                    sshagent(['SSHEC2']) {
                        // SSH into the Docker EC2 instance
                        // Copy the Dockerfile to the Docker EC2 instance
                        sh "scp -o StrictHostKeyChecking=no Dockerfile ubuntu@ec2-54-152-159-155.compute-1.amazonaws.com:/home/ubuntu/Dockerfile"
                        sh "scp -o StrictHostKeyChecking=no -r target/ Dockerfile ubuntu@ec2-54-152-159-155.compute-1.amazonaws.com:/home/ubuntu/"                       
            
                        // SSH into the Docker EC2 instance and build the Docker image
                        sh "ssh -o StrictHostKeyChecking=no ubuntu@ubuntu@ec2-54-152-159-155.compute-1.amazonaws.com 'cd /home/ubuntu/ && docker image build -t ${DockerHubUser}/${ImageName}:${ImageTag} -f Dockerfile .'"
                        // sh "ssh -o StrictHostKeyChecking=no ubuntu@ec2-54-152-159-155.compute-1.amazonaws.com 'cd /path/to/dockerfile && docker image build -t ${Dockeraccount}/${ImageName}:${ImageTag} .'"
                    }   
                }
            }
        }

    }
}
