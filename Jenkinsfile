pipeline{
    
    agent any

    stages{

        stage('Git Checkout') {

            steps{

                script{

                    git branch: 'main', url: 'https://github.com/zohera27/devops_Java_Project.git'
                }
            }
        }
    }
}