pipeline {
    agent any
    stages {
        stage('Build') {
            steps {
                sh '''
                docker build -t gcr.io/lbg-python-cohort-8/piers-python-api:latest .
                '''
            }
        }
        stage('Push') {
            steps {
                sh '''
                docker push gcr.io/lbg-python-cohort-8/piers-python-api:latest
                '''
            }
        }
        stage('Deploy') {
            steps {
                sh '''
                kubectl apply -f ./kubernetes/
                kubectl rollout restart deployment backend
                kubectl rollout restart deployment nginx
                '''
            }
        }
        stage('Clean Up') {
            steps {
                sh '''
                docker system prune -a --force
                '''
            }
        }
    }
}
