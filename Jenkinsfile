pipeline {
    agent any
    stages {
        stage('Build App') {
            steps {
                sh 'echo "Building Sa-Frontend"'
                sh 'cd ${WORKSPACE}/sa-frontend && npm install && npm run build'
                sh 'echo "Building Sa-webapp"'
                sh 'cd ${WORKSPACE}/sa-webapp && mvn install'
            }
        }
        stage('Build Images') {
            steps {
                sh 'echo "Creating fronted Image"'
                sh 'cd ${WORKSPACE}/sa-frontend && docker build -t sa-frontend:"$BUILD_NUMBER" .'
                sh 'echo "Frontend Image created"'
                sh 'echo "Creating webapp Image"'
                sh 'cd ${WORKSPACE}/sa-webapp && docker build -t sa-webapp:"$BUILD_NUMBER" .'
                sh 'echo "Webapp Image Created"'
                sh 'echo "Creating sa-logic image"'
                sh 'cd ${WORKSPACE}/sa-logic && docker build -t sa-logic:"$BUILD_NUMBER" .'
                sh 'echo "sa-logic image created"'

            }
        }
        stage('push to harbor-dev'){
            when {
                branch 'develop'
                }
            steps {
                withDockerRegistry([ credentialsId: "harbor-cred", url: "http://harbor.devopsdoor.com" ]){
                sh 'docker tag sa-frontend:"$BUILD_NUMBER" http://harbor.devopsdoor.com/cicd_dev/sa-frontend:"$BUILD_NUMBER"'
                sh 'docker tag sa-webapp:"$BUILD_NUMBER" harbor.devopsdoor.com/cicd_dev/sa-webapp:"$BUILD_NUMBER"'
                sh 'docker tag sa-frontend:"$BUILD_NUMBER" harbor.devopsdoor.com/cicd_dev/sa-logic:"$BUILD_NUMBER"'
                sh 'docker push http://harbor.devopsdoor.com/cicd_dev/sa-frontend:"$BUILD_NUMBER"'
                sh 'docker push harbor.devopsdoor.com/cicd_dev/sa-webapp:"$BUILD_NUMBER"'
                sh 'docker push harbor.devopsdoor.com/cicd_dev/sa-logic:"$BUILD_NUMBER"'
                }
            }
        }
        stage('push to harbor-prod'){
            when {
                branch 'master'
                }
            steps {
                withDockerRegistry([ credentialsId: "harbor-cred", url: "http://harbor.devopsdoor.com" ]){
                sh 'docker tag sa-frontend:"$BUILD_NUMBER" harbor.devopsdoor.com/cicd-prod/sa-frontend:"$BUILD_NUMBER"'
                sh 'docker tag sa-webapp:"$BUILD_NUMBER" harbor.devopsdoor.com/cicd-prod/sa-webapp:"$BUILD_NUMBER"'
                sh 'docker tag sa-frontend:"$BUILD_NUMBER" harbor.devopsdoor.com/cicd-prod/sa-logic:"$BUILD_NUMBER"'
                sh 'docker push harbor.devopsdoor.com/cicd-prod/sa-frontend:"$BUILD_NUMBER"'
                sh 'docker push harbor.devopsdoor.com/cicd-prod/sa-webapp:"$BUILD_NUMBER"'
                sh 'docker push harbor.devopsdoor.com/cicd-prod/sa-logic:"$BUILD_NUMBER"'
                }
            }
        }

    }
}