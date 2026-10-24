```groovy
pipeline {
    agent any

    stages {
        stage('Checkout') {
            steps {
                echo 'Source code checked out from GitHub'
            }
        }

        stage('Build') {
            steps {
                echo 'Building the DevOps Practical Lab application'
            }
        }

        stage('Test') {
            steps {
                sh 'python3 --version'
                sh 'python3 -m py_compile app.py test_app.py'
                echo 'Python syntax checks passed'
            }
        }
    }

    post {
        success {
            echo 'Pipeline completed successfully'
        }
        failure {
            echo 'Pipeline failed'
        }
    }
}
```
