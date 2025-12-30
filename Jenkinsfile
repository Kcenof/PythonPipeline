pipeline {
    agent any

    environment {
        DOCKER_IMAGE = 'skabserhii/python-lab-app'
        DOCKER_CREDS = 'docker-hub-credentials'
    }

    stages {
        stage('Checkout') {
            steps {
                echo 'Скачуємо код...'
                checkout scm
            }
        }

        stage('Test') {
            steps {
                bat '"C:/Users/ymrfe/AppData/Local/Python/bin/python.exe" test_app.py'
            }
        }

        stage('Build Docker Image') {
            steps {
                script {
                    echo 'Створюємо Docker образ...'
                    bat "docker build -t ${DOCKER_IMAGE}:latest ."
                }
            }
        }

        stage('Push to Docker Hub') {
            steps {
                script {
                    echo 'Заходимо в Docker Hub і відправляємо...'
                    
                    withCredentials([usernamePassword(credentialsId: DOCKER_CREDS, usernameVariable: 'USER', passwordVariable: 'PASS')]) {
                       
                        bat "docker login -u %USER% -p %PASS%"
                     
                        bat "docker push ${DOCKER_IMAGE}:latest"
                    }
                }
            }
        }
        
        stage('Cleanup') {
            steps {
                
                 bat "docker rmi ${DOCKER_IMAGE}:latest"
                 bat "docker logout"
            }
        }
    }
}
