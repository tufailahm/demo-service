node {
    def mvnHome = tool 'MyMaven'
    def dockerImageTag = "8867205331/dockerhub{env.BUILD_NUMBER}"
    stage('clone repo'){
        git 'https://github.com/tufailahm/demo-service.git'
        mvnHome = tool 'MyMaven'
    }
    stage('Build demoservice project'){
        //sh    linux
        bat "H:\\apache-maven-3.8.2-bin\\apache-maven-3.8.2\\bin\\mvn clean install"
        //jar file will be generated
    }
    stage('Build docker image'){
        dockerImage = docker.build("8867205331/dockerhub:${env.BUILD_NUMBER}")
    }
    stage('Build docker deploy'){
        echo "Docker Image Tag name : ${dockerImageTag}"
        //docker-hub-credentials - we have to create in jenkins credentials
        docker.withRegistry('https://registry.hub.docker.com','docker-hub-credentials') {
            dockerImage.push("${env.BUILD_NUMBER}")
            dockerImage.push("latest")
        }
    }
}