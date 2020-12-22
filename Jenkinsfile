pipeline {
    agent any
    stages {
        stage('Build') {
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
                sh 'echo "Creating webapp Image'
                sh 'cd ${WORKSPACE}/sa-webapp && docker build -t sa-webapp:"$BUILD_NUMBER" .'
                sh 'echo "Creating sa-logic image'
                sh 'cd ${WORKSPACE}/sa-logic && docker build -t sa-logic:"$BUILD_NUMBER" .'

            }
        }
        stage('push to dockerhub'){
            steps {
                withDockerRegistry([ credentialsId: "dockerhub", url: "" ]){
                sh 'docker tag sa-frontend:"$BUILD_NUMBER" devopsdoor/sa-frontend:"$BUILD_NUMBER"'
                sh 'docker tag sa-webapp:"$BUILD_NUMBER" devopsdoor/sa-webapp:"$BUILD_NUMBER"'
                sh 'docker tag sa-logic:"$BUILD_NUMBER" devopsdoor/sa-logic:"$BUILD_NUMBER"'
                sh 'docker push devopsdoor/sa-frontend:"$BUILD_NUMBER"'
                sh 'docker push devopsdoor/sa-webapp:"$BUILD_NUMBER"'
                sh 'docker push devopsdoor/sa-logic:"$BUILD_NUMBER"'
                }
            }
        }
        stage('push to harbor'){
            when {
                branch 'develop'
                }
            steps {
                withDockerRegistry([ credentialsId: "harbor", url: "https://harbor.postelic.com" ]){
                sh 'docker tag sa-frontend:"$BUILD_NUMBER" harbor.postelic.com/harbor-dev/sa-frontend:"$BUILD_NUMBER"'
                sh 'docker tag sa-webapp:"$BUILD_NUMBER" harbor.postelic.com/harbor-dev/sa-webapp:"$BUILD_NUMBER"'
                sh 'docker tag sa-logic:"$BUILD_NUMBER" harbor.postelic.com/harbor-dev/sa-logic:"$BUILD_NUMBER"'
                sh 'docker push harbor.postelic.com/harbor-dev/sa-frontend:"$BUILD_NUMBER"'
                sh 'docker push harbor.postelic.com/harbor-dev/sa-webapp:"$BUILD_NUMBER"'
                sh 'docker push harbor.postelic.com/harbor-dev/sa-logic:"$BUILD_NUMBER"'
                }
            }
            when {
                branch 'master'
                }
            steps {
                withDockerRegistry([ credentialsId: "harbor", url: "https://harbor.postelic.com" ]){
                sh 'docker tag sa-frontend:"$BUILD_NUMBER" harbor.postelic.com/harbor-prod/sa-frontend:"$BUILD_NUMBER"'
                sh 'docker tag sa-webapp:"$BUILD_NUMBER" harbor.postelic.com/harbor-prod/sa-webapp:"$BUILD_NUMBER"'
                sh 'docker tag sa-logic:"$BUILD_NUMBER" harbor.postelic.com/harbor-prod/sa-logic:"$BUILD_NUMBER"'
                sh 'docker push harbor.postelic.com/harbor-prod/sa-frontend:"$BUILD_NUMBER"'
                sh 'docker push harbor.postelic.com/harbor-prod/sa-webapp:"$BUILD_NUMBER"'
                sh 'docker push harbor.postelic.com/harbor-prod/sa-logic:"$BUILD_NUMBER"'
                }
            }
        }
    }  
  }
}