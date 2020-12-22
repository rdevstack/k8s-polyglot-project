pipeline {
    agent any

    stages {
        stage('Build Sa-Frontend') {
            steps {
                sh 'cd ${WORKSPACE}/sa-frontend && npm install && npm run build'
            }
        }
        stage('Build Sa-Webapp') {
            steps {
                sh 'cd ${WORKSPACE}/sa-webapp && mvn install'
            }
        }
        stage('Containerize sa-frontend') {
            steps {
                sh 'cd ${WORKSPACE}/sa-frontend && docker build -t sa-frontend:1.0.0 .'
            }
        }
        stage('Containerize sa-Webapp') {
            steps {
                sh 'cd ${WORKSPACE}sa-webapp && docker build -t sa-webapp:1.0.0 .'
            }
        }
        stage('Containerize sa-logic') {
            steps {
                sh 'cd ${WORKSPACE}sa-logic && docker build -t sa-logic:1.0.0 .'
            }
        }
        stage('push to dockerhub'){
            steps {
                sh 'docker tag sa-frontend devopsdoor/sa-frontend'
                sh 'docker tag sa-webapp devopsdoor/sa-webapp'
                sh 'docker tag sa-logic devopsdoor/sa-logic'
                sh 'docker push devopsdoor/sa-frontend'
                sh 'docker push devopsdoor/sa-webapp'
                sh 'docker push devopsdoor/sa-logic'
            }
        }

        
	}
    }
}
