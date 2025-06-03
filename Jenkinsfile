pipeline {
    agent any
    stages {
        stage('Build') {
            steps {
                #sh 'mvn clean package -DskipTests'
                sh 'docker build -t fleetman-webapp:latest .'
            }
        }
        stage('Quality Check') {
            steps {
                withSonarQubeEnv('SonarQube') {
                    sh 'mvn sonar:sonar'
                }
            }
        }
        stage('Deploy') {
            steps {
                sh 'kubectl apply -f manifests/'
            }
        }
    }
    post {
        always {
            echo 'Pipeline terminé.'
        }
        success {
            echo 'Déploiement réussi !'
        }
        failure {
            echo 'Échec du pipeline. Vérifiez les logs.'
        }
    }
}
