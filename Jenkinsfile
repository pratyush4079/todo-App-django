pipeline {
    agent any

    environment {
  
        PYTHON_ENV = 'venv'
        REPO_PATH = 'E:\\jenkins_pipeline\\todo-App-django'  
        BRANCH_NAME = 'release/testing-jenkins'        // Branch you want to checkout
        VIRTUAL_ENV= 'E:\\jenkins_pipeline\\venv\\todoApp\\Scripts'
    }


    stages {
        //  stage('Configure Git Safe Directory') {
        //     steps {
        //         script {
        //             // Add the repository directory to the safe list
        //             bat "git config --global --add safe.directory ${REPO_PATH}"
        //         }
        //     }
        // }
       stage('Checkout') {
            steps {
                script {
                    dir(env.REPO_PATH) {
                        bat "dir" 
                    }
                }
            }
        }

        stage('Setup Python Environment') {
            steps {
                script {
                    if (!fileExists("${env.PYTHON_ENV}")) {
                        bat 'python -m venv venv'
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

        stage('Build') {
            steps {
                sh '''
                source venv/bin/activate
                python manage.py runserver
                '''
            }
        }
    }

    post {
        always {
            cleanWs()
        }
    }
}