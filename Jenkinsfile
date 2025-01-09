pipeline {
    agent any

    stages {
        stage('Debugging Path') {
            steps {
                script {
                    // Transform workspace path to Docker-compatible format
                    def transformedPath = env.WORKSPACE.replace('\\', '/').replace('C:', '/c')
                    echo "Transformed Workspace Path: ${transformedPath}"
                }
            }
        }

        stage('Building JARs') {
            agent {
                docker {
                    image 'maven:3.9.3-eclipse-temurin-17-focal'
                    args "-v ${env.WORKSPACE.replace('\\', '/').replace('C:', '/c')}:/workspace -w /workspace -u root -v /tmp/m2:/root/.m2"
                }
            }
            steps {
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
