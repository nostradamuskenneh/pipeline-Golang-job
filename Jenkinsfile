pipeline {
    agent any 

    tools {
        // Define tool name and version
        maven 'Maven3'
        jdk 'JDK8'
    }

    stages {
        stage('Checkout') {
            steps {
                // Checkout the code from the SCM
                checkout scm
            }
        }

        stage('Build') {
            steps {
                // Build the code using Maven
                sh 'mvn clean install -DskipTests'
            }
        }

        stage('Archive') {
            steps {
                // Archive the build artifacts
                arctifacts: '**/target/*.jar', allowEmptyArchive: true
            }
        }

        stage('Test') {
            steps {
                // Run the unit tests
                sh 'mvn test'
            }
        }
    }

    post {
        always {
            // Cleanup after the build
            deleteDir()
        }
        success {
            echo 'Build was successful!'
        }
        failure {
            echo 'Blded!'
        }
    }
}
