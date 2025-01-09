pipeline {
    agent any

    stages {
        stage('Building JARs') {
            agent {
                docker {
                    image 'maven:3.9.3-eclipse-temurin-17-focal'
                    args "-v ${env.WORKSPACE.replace('\\', '/').replace('C:', '/c')}:/workspace -w /workspace"
                }
            }
            steps {
                sh "mvn clean package -DskipTests"
            }
        }

        stage('Creating an Image') {
            steps {
                script {
                    app = docker.build('apurvanaik422/seldocker100')
                }
            }
        }

        stage('Pushing Image to DockerHub') {
            steps {
                script {
                    docker.withRegistry('', 'dockercred') {
                        app.push('latest')
                    }
                }
            }
        }
    }
}
