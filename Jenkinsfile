pipeline {
    agent any

    parameters {
        booleanParam(name: 'executeTests', defaultValue: true, description: 'Run Test Stage')
    }

    environment {
        VERSION = '1.0.0'
        DEPLOY_ENV = 'staging'
    }

    tools {
        maven 'Maven 3.8.5'
    }

    stages {

        stage('Build') {
            steps {
                echo "Building version ${VERSION}"
                bat 'mvn -v'
                bat 'mvn clean install'
            }
        }

        stage('Test') {
            when {
                expression { return params.executeTests == true }
            }
            steps {
                echo 'Running tests...'
                bat 'mvn test'
            }
        }

        stage('Deploy') {
            steps {
                echo "Deploying to ${DEPLOY_ENV} environment"
                bat 'echo Simulating deploy step...'
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
            echo 'Build failed.'
        }
    }
}
