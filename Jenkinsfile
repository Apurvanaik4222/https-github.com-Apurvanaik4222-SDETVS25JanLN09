pipeline {
    agent any

    stages {
        stage('Building jars') {
            steps {
                bat "mvn clean package -DskipTests"
            }
        }

        stage('Creating an Image') {
            steps {
                bat "docker build -t selenium/docker100 ."
            }
        }

        stage('Pushing Image to DockerHub') {
            environment {
                DOCKER_HUB = credentials('docker_cred') // Credentials ID for DockerHub
            }

            steps {
                // Logging into DockerHub using credentials
                bat 'docker login -u %DOCKER_HUB_USR% -p %DOCKER_HUB_PSW%'
                bat "docker push selenium/docker100"
            }
        }
    }
}
