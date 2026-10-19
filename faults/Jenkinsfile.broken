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
            steps { bat 'py scripts/check_app.py' }
        }
        stage('Package Release') {
            steps { bat 'py scripts/build_releases.py' }
        }
        stage('Archive Release') {
            steps { archiveArtifacts artifacts: 'dist/*.zip', fingerprint: true }
        }
        stage('Build Metadata') {
            steps {
                bat 'echo Build Number: %BUILD_NUMBER% > build-info.txt'
                archiveArtifacts artifacts: 'build-info.txt'
            }
        }
    }
}
