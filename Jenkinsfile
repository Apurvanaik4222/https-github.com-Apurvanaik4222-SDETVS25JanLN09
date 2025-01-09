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
                    args "-v ${env.WORKSPACE.replace('\\', '/').replace('C:', '/c')}:/workspace -w /workspace"
