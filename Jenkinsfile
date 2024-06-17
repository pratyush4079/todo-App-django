pipeline {
    agent any

    environment {
        // Define any environment variables here
        PYTHON_ENV = 'venv'
    }

    stages {
        stage('Checkout') {
            steps {
                git 'https://github.com/pratyush4079/todo-App-django.git'
            }
        }

        stage('Setup Python Environment') {
            steps {
                script {
                    if (!fileExists("${env.PYTHON_ENV}")) {
                        sh 'python3 -m venv venv'
                    }
                }
            }
        }

        stage('Install Dependencies') {
            steps {
                sh '''
                source venv/bin/activate
                pip install -r requirements.txt
                '''
            }
        }

        stage('Run Tests') {
            steps {
                sh '''
                source venv/bin/activate
                python manage.py test
                '''
            }
        }

        stage('Build and Deploy') {
            steps {
                sh '''
                source venv/bin/activate
                python manage.py collectstatic --noinput
                '''
                // Add deployment steps here if any
            }
        }
    }

    post {
        always {
            cleanWs()
        }
    }
}
