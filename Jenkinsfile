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
                bat "docker build -t apurvanaik422/seldocker100 ."
            }
        }

        stage('Pushing Image to DockerHub') {
            steps {
                // Use the withCredentials block to inject the credentials into the environment variables
                withCredentials([usernamePassword(credentialsId: 'docker_credL', usernameVariable: 'DOCKER_USERNAME', passwordVariable: 'DOCKER_PASSWORD')]) {
                    // Perform Docker login using the credentials
                    bat "echo %DOCKER_PASSWORD% | docker login -u %DOCKER_USERNAME% --password-stdin"
                }
            }
        }
    }

    post {
        always {
            // Logout from DockerHub after pipeline execution
            bat "docker logout"
        }
    }
}
