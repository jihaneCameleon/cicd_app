node {   
    stage('Clone repository') {
        git credentialsId: 'git', url: 'https://github.com/amachlou/cicd_app'
    }
    
    stage('Build image') {
       dockerImage = docker.build("amachlou/cicd_app:"+ "$BUILD_NUMBER")
    }
    
    stage('Push image') {
        withDockerRegistry([ credentialsId: "docker_hub", url: "" ]) {
        dockerImage.push()
        }
    }    
}