pipeline {
    agent any

    // Define parameters
    parameters {
        booleanParam(name: 'executeTests', defaultValue: true, description: 'Run Test Stage')
    }

    // Define environment variables
    environment {
        VERSION = '1.0.0'
        DEPLOY_ENV = 'staging'
    }

    // Use tools (Make sure Maven is configured with this name in Jenkins)
    tools {
        maven 'Maven 3.8.5'
    }

    stages {

        stage('Build') {
            steps {
                echo "Building version ${VERSION}"
                sh 'mvn clean install'  // use bat 'mvn clean install' on Windows
            }
        }

        stage('Test') {
            when {
                expression { return params.executeTests == true }
            }
            steps {
                echo 'Running Tests...'
                sh 'mvn test'  // use bat 'mvn test' on Windows
            }
        }

        stage('Deploy') {
            steps {
                echo "Deploying to ${DEPLOY_ENV} environment"
                // Add deploy commands here
            }
        }
    }

    post {
        always {
            echo 'Pipeline has completed (success or failure).'
        }
        success {
            echo 'Build was successful!'
        }
        failure {
            echo 'Build failed!'
        }
    }
}
