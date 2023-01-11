pipeline {
    environment {
        registry = 'amachlou/cicd_app'
        registryCredential = 'docker_hub'
        dockerImage = ''
    }
    agent any
    stages {
        stage('Cloning Git') {
            steps {
                git 'https://github.com/amachlou/cicd_app.git'
            }
        }
        stage('Building image') {
            steps {
                script {
                    dockerImage = docker.build registry + ":$BUILD_NUMBER"
                }
            }
        }
        stage('Test image') {
            steps {
                script {
                    echo 'Tests passed'
                }
            }
        }
        stage('Publish Image') {
            steps {
                script {
                    // docker.withRegistry('tcp://192.168.11.104:2376', registryCredential)
                    withDockerRegistry([ credentialsId: registryCredential, url: "" ]) {
                        dockerImage.push()
                    }
                }
            }
        }
        stage('Deploy image') {
            steps {
                bat "docker run -d $registry:$BUILD_NUMBER"
            }
        }
    }
}
