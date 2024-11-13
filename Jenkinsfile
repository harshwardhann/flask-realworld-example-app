pipeline {
    agent any
    environment {
       `FLASK_APP = ${WORKSPACE}/autoapp.py`  // Jenkins workspace path
        FLASK_DEBUG = '1'
        CONDUIT_SECRET = 'something-really-secret'
    }
    stages {
        stage('Clone Repository') {
            steps {
                // Clone the Flask app from GitHub
                git 'https://github.com/harshwardhann/flask-realworld-example-app.git'
            }
        }
        stage('Install Dependencies') {
            steps {
                // Install the required dependencies
                script {
                    sh 'pip install -r requirements/dev.txt'
                }
            }
        }
        stage('Database Migrations') {
            steps {
                // Run the Flask database migrations
                script {
                    sh 'flask db init'
                    sh 'flask db migrate'
                    sh 'flask db upgrade'
                }
            }
        }
        stage('Run Tests') {
            steps {
                // Run the Flask tests
                script {
                    sh 'flask test'
                }
            }
        }
    }
    post {
        always {
            // Clean up or notify on success/failure
            echo 'Pipeline execution completed.'
        }
    }
}
