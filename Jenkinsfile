pipeline {
    agent any
    environment {
        IMAGE_NAME = "todo-flask"
        CONTAINER_NAME = "todo-container"
    }
    stages {
        stage('Clone') {
            steps {
                git url: 'https://github.com/PradeepYadav90/flask_todo_pipeline.git' ,branch:'main'
            }
        }
        stage('Build') {
            steps {
                script {
                    docker.build("${IMAGE_NAME}")
                }
            }
        }
        stage('Deploy') {
            steps {
                script {
                    sh "docker stop ${CONTAINER_NAME} || true"
                    sh "docker rm ${CONTAINER_NAME} || true"
                    sh "docker run -d -p 5000:5000 --name ${CONTAINER_NAME} ${IMAGE_NAME}"
                }
            }
        }
    }
}
