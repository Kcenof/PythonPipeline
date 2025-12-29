pipeline {
    agent any

    stages {
        stage('Checkout') {
            steps {
                // Jenkins сам скачає код з Git
                echo 'Code checkout complete'
            }
        }
        
        stage('Test') {
            steps {
                // Запускаємо тести через Python
                bat '"C:\Users\ymrfe\AppData\Local\Microsoft\WindowsApps\python.exe" test_app.py'
            }
        }
    }
}
