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
            environment {
                DOCKER_HUB = credentials('docker_cred') // Use Jenkins credentials for DockerHub
            }

            steps {
                // Print out the variables for debugging (avoid printing passwords in production)
                bat 'echo %DOCKER_HUB_USR%'
                bat 'echo %DOCKER_HUB_PSW%'

                // Secure login to DockerHub using --password-stdin
                script {
                    withEnv(["DOCKER_USERNAME=%DOCKER_HUB_USR%", "DOCKER_PASSWORD=%DOCKER_HUB_PSW%"]) {
                        bat 'echo %DOCKER_PASSWORD% | docker login -u %DOCKER_USERNAME% --password-stdin'
                    }
                }

                // Push the image to DockerHub
                bat "docker push apurvanaik422/seldocker100"
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
