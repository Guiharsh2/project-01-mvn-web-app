pipeline {
    agent any

    tools {
        maven 'Maven-3.9.0'   // Configure in Jenkins: Manage Jenkins -> Tools
        jdk 'JDK-11'          // Same here for JDK
    }

    stages {
        stage('Checkout') {
            steps {
                echo 'Fetching source code...'
                checkout scm
            }
        }

        stage('Build') {
            steps {
                echo 'Building application...'
                sh 'mvn clean install -Dmaven.test.skip=true'
            }
        }

        stage('Test') {
            steps {
                echo 'Running unit tests...'
                sh 'mvn test'
            }
        }

        stage('Package') {
            steps {
                echo 'Packaging WAR file...'
                sh 'mvn package'
            }
        }

        stage('Deploy') {
            steps {
                echo 'Deploying application...'
                sh 'cp target/*.war /opt/tomcat/webapps/'  // Example: deploy to Tomcat
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
