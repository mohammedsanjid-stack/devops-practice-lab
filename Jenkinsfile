
pipeline {
    agent any

    stages {
        stage('Checkout') {
            steps {
                checkout scm
            }
        }

        stage('Test') {
            steps {
                sh '''
                    python3 -m venv .venv
                    . .venv/bin/activate
                    python -m pip install --upgrade pip
                    pip install -r requirements.txt
                    pip install pytest
                    pytest -v
                '''
            }
        }

        stage('Build & Push') {
            steps {
                withCredentials([usernamePassword(
                    credentialsId: 'dockerhub-creds',
                    usernameVariable: 'DOCKERHUB_USER',
                    passwordVariable: 'DOCKERHUB_TOKEN'
                )]) {
                    sh '''
                        docker build -t mhdsanjid/devops-mastery-app:${BUILD_NUMBER} .
                        docker tag mhdsanjid/devops-mastery-app:${BUILD_NUMBER} mhdsanjid/devops-mastery-app:latest

                        echo "$DOCKERHUB_TOKEN" | docker login -u "$DOCKERHUB_USER" --password-stdin

                        docker push mhdsanjid/devops-mastery-app:${BUILD_NUMBER}
                        docker push mhdsanjid/devops-mastery-app:latest

                        docker logout
                    '''
                }
            }
        }
    }

    post {
        success {
            echo 'Tests passed and Docker images were pushed successfully.'
        }
        failure {
            echo 'Pipeline failed. Check the console output.'
        }
    }
}
