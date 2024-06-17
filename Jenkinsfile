pipeline {
    agent any

    environment {
        // Define any environment variables here
        PYTHON_ENV = 'venv'
        REPO_PATH = 'E:\\jenkins_pipeline\\todo-App-django'  // Path to your local repository
        BRANCH_NAME = 'release/testing-jenkins'        // Branch you want to checkout
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
                    // Navigate to the repository directory
                    dir(env.REPO_PATH) {
                        // Checkout the specified branch
                        bat "dir" // for windows , sh doesnt work
                    }
                }
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