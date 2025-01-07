pipeline{
agent any

stages{
    stage('Building jars'){

        steps{

            bat "mvn clean package -DskipTests"
        }
    }

    stage('Creating an Image'){

        steps{

            bat "docker build -t apurvanaik422/seldocker100 ."
        }
    }

    stage('Pushing Image to DockerHub'){

        environment{
            DOCKER_HUB =credentials('docker_cred')
        }

        steps{
            //docker login -u $(DOCKER_HUB_USR) -p $(DOCKER_HUB_PSW)  --linux
            bat 'docker login -u %DOCKER_HUB_USR% -p %DOCKER_HUB_PSW%'
            bat "docker push apurvanaik422/seldocker100"
        }

    }


}

}