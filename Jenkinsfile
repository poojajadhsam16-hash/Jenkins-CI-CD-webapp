pipeline {

    agent any

    stages {

        stage('Build') {
            steps {
                echo 'Building Docker image...'

                bat 'docker build -t task2-jenkins-app:%BUILD_NUMBER% .'
            }
        }

        stage('Test') {
            steps {
                echo 'Testing Docker image...'

                bat 'docker image inspect task2-jenkins-app:%BUILD_NUMBER%'
            }
        }

        stage('Deploy') {
            steps {
                echo 'Deploying application...'

                bat 'docker rm -f task2-jenkins-app 2>nul || exit /b 0'

                bat 'docker run -d --name task2-jenkins-app -p 8081:80 task2-jenkins-app:%BUILD_NUMBER%'
            }
        }
    }

    post {
        success {
            echo 'CI/CD Pipeline completed successfully!'
        }

        failure {
            echo 'CI/CD Pipeline failed. Check the console output.'
        }
    }
}
