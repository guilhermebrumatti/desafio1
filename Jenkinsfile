pipeline {
    agent {
        label 'main'
    }

    environment {
	    DOCKERHUB_CREDENTIALS = '<PASSWORD>'
	}


    stages{
        stage('Clone repository') {
            steps{
                checkout([$class: 'GitSCM', branches: [[name: '*/main']], browser: [$class: 'GithubWeb', repoUrl: 'https://github.com/guilhermebrumatti/desafio1.git'], extensions: [], userRemoteConfigs: [[credentialsId: 'NONE', url: 'https://github.com/guilhermebrumatti/desafio1.git']]])
            }
            
        }

        stage('Build') {
            steps{
                
                bat 'docker build -t guilhermebrumatti/desafio1:latest https://github.com/guilhermebrumatti/desafio1'
            }
        }
        stage('Login to dockerhub') {
            steps{
                bat 'docker login -u <USERNAME> -p <PASSWORD>'
            }    
        }
        stage('Push image') {
            steps{
                bat 'git push https://github.com/guilhermebrumatti/desafio1 HEAD:main'
            }  
        post {
            always {
               bat 'docker logout' 
            }
        }         
            
        }
    }
}
