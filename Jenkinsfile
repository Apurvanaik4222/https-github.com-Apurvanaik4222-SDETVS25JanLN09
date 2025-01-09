pipeline {
    agent any

    stages {
        stage('Building JARs') {
            agent {
                docker {
                    image 'maven:3.9.3-eclipse-temurin-17-focal'
                    args '-v ${WORKSPACE}:/workspace -w /workspace'
                }
            }
            steps {
                // Build the project using Maven
                sh "mvn clean package -DskipTests"
            }
        }

        stage('Creating an Image') {
            steps {
                script {
                    // Build the Docker image
                    app = docker.build('apurvanaik422/seldocker100')
                }
            }
        }

        stage('Pushing Image to DockerHub') {
            steps {
                script {
                    docker.withRegistry('', 'dockercred') {
                        // Push the image with the 'latest' tag
                        app.push('latest')
                    }
                }
            }
        }
    }
}
