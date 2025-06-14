pipeline {
    agent any

    stages {
        stage('Install Dependencies') {
            steps {
                bat 'npm install'
            }
        }

        stage('Run Tests') {
            steps {
                bat 'npm test'
            }
        }

        stage('Security Scan') {
            steps {
                bat 'dependency-check --project "SafeNotes" --scan . --format "HTML"'
            }
        }
    }

    post {
        always {
            archiveArtifacts artifacts: 'dependency-check-report.html', allowEmptyArchive: true
        }
    }
}