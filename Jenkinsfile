pipeline {
    agent any

    stages {
        stage('Checkout') {
            steps {
                // Checkout the code from the Git repository
                git branch: 'main', url: 'https://github.com/campinwa/ExpenseManager.git'
            }
        }

        stage('Build') {
            steps {
                // Run the Maven build
                sh 'mvn clean package'
            }
        }

        stage('Test') {
            steps {
                // Run the Maven tests
                sh 'mvn test'
            }
        }

        stage('Deploy') {
            steps {
                // Deploy the application
                // You can add deployment steps here, e.g., copying files, running scripts, etc.
                echo 'Deploying application...'
                // sh 'scp target/your-app.war user@server:/path/to/deploy'
            }
        }
    }

    post {
        always {
            // Archive the build artifacts
            archiveArtifacts artifacts: 'target/*.jar', allowEmptyArchive: true

            // Publish test results
            junit 'target/surefire-reports/*.xml'
        }

        failure {
            // Notify if the build fails
            echo 'Build failed!'
        }

        success {
            // Notify if the build succeeds
            echo 'Build succeeded!'
        }
    }
}
