pipeline {
    agent any
    stages {
        stage('Build') {
            steps {
                sh 'docker build -t fleetman-webapp:latest .'
            }
        }
        stage('Deploy') {
            steps {
                sh 'kubectl apply -f manifests/'
            }
        }
    }
}
