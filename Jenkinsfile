pipeline {
    agent any

    stages {

        stage('Build') {
            steps {
                sh 'mvn clean package'
            }
        }

        stage('Docker Build') {
            steps {
                sh 'docker build -t springboot-devops-demo:v1 .'
            }
        }

        stage('Docker Push') {
            steps {
                sh '''
                docker tag springboot-devops-demo:v1 8885257761/springboot-devops-demo:v1
                docker push 8885257761/springboot-devops-demo:v1
                '''
            }
        }

        stage('Deploy') {
            steps {
                sh '''
                docker pull 8885257761/springboot-devops-demo:v1
                docker rm -f springboot-app || true
                docker run -d --name springboot-app -p 8081:8080 8885257761/springboot-devops-demo:v1
                '''
            }
        }
    }
}
