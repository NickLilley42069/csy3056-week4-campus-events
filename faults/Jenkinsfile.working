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
            steps { bat 'py scripts/build_release.py' }
        }
        stage('Archive Release') {
            steps { archiveArtifacts artifacts: 'dist/*.zip', 
                    fingerprint: true }
        }
        stage('Build Metadata') {
            steps { bat 'echo Build Number: 22 > build-info.txt'
                        archiveArtifacts artifacts: 'dist/campus-event-1.1.0.zip, build-info.txt'}
        }
    }
}
