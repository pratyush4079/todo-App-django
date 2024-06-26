pipeline {
    agent any

    stages {
        stage('Checkout') {
            steps {
                git branch: 'release/testing-jenkins', url: 'https://github.com/pratyush4079/todo-App-django'
            }
        }

        stage('Setup') {
            steps {
               bat '''
                REM Install dependencies
                python -m venv testing
                .\\testing\\Scripts\\activate
                pip install -r requirements.txt
                '''
            }
        }

        stage('Run Migrations') {
            steps {
                sh '''
                # Apply migrations
                python manage.py migrate
                '''
            }
        }

        stage('Run Tests') {
            steps {
                sh '''
                # Run tests
                python manage.py test
                '''
            }
        }

        stage('Run Server') {
            steps {
                sh '''
                # Run the Django server
                python manage.py runserver 0.0.0.0:8000 &
                '''
            }
        }
    }
}
