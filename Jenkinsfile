pipeline {
    agent any
    options { skipDefaultCheckout(true) }
    stages {
        stage('Checkout') {
            steps { checkout scm }
        }
        stage('Setup') {
            steps { bat 'py --version' }
        }
        stage('Validate Application') {
            steps { bat  'py scripts/check_app.py' }
        }
        stage("Package Release") {
            steps { bat "python scripts / build_release.py"}
        }
        stage("Archive Release") {
            steps { bat "archiveArtifacts artifacts: 'dist/*.zip', fingerprint: true"}
        }
    }
}
