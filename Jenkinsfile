pipeline {
    agent any
    environment {
        SONARQUBE = 'sonarqubesample' // The name of the SonarQube server configured in Jenkins
        GIT_REPO = 'https://github.com/akhilreddy1420/cicdhtml.git' // Your GitHub repo URL
        DEPLOY_DIR = '/var/www/html' // Apache2 document root directory
    }
    stages {
        stage('Checkout') {
            steps {
                // Checkout code from GitHub (HTML files)
                git branch: 'main', url: "${GIT_REPO}"
            }
        }
        
        stage('SonarQube Analysis') {
            steps {
                // Run SonarQube analysis on HTML files (optional but recommended)
                script {
                    sh 'sonar-scanner -Dsonar.projectKey=your_project_key -Dsonar.host.url=http://54.209.229.51:9000 -Dsonar.sources=.'
                }
            }
        }

        stage('Deploy to Apache') {
            steps {
                script {
                    // Deploy the HTML files to Apache2's document root
                    sh 'cp -r * ${DEPLOY_DIR}/'
                }
            }
        }
    }
    post {
        success {
            echo 'Pipeline successfully completed!'
        }
        failure {
            echo 'Pipeline failed. Check the logs.'
        }
    }
}
