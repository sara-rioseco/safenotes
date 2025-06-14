pipeline {
    agent any

    stages {
        stage('Check Environment') {
            steps {
                bat 'where npm || echo "npm not found"'
                bat 'npm -v'
                bat 'node -v'
            }
        }

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
                bat 'dependency-check --project "SafeNotes" --scan . --format "HTML" --out . --outfile dependency-check-report'
            }
        }
    }

    post {
        always {
            archiveArtifacts artifacts: 'dependency-check-report.html', allowEmptyArchive: true
        }
    }
}