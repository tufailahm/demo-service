node {
	    // reference to maven
	    // ** NOTE: This 'maven-3.5.2' Maven tool must be configured in the Jenkins Global Configuration.
	    def mvnHome = tool 'MyMaven'


	    // holds reference to docker image
	    def dockerImage
	    // ip address of the docker private repository(nexus)

	    def dockerImageTag = "8867205331/dockerhub{env.BUILD_NUMBER}"

	    stage('Clone Repo') { // for display purposes
	      // Get some code from a GitHub repository
	      git 'https://github.com/tufailahm/demo-service.git'
	      // Get the Maven tool.
	      mvnHome = tool 'MyMaven'
	    }

	    stage('Build Project') {
	      // build project via maven
	      bat "H:\\apache-maven-3.8.2-bin\\apache-maven-3.8.2\\bin\\mvn clean install"
	    }

	    stage('Build Docker Image') {
	      // build docker image
	      dockerImage = docker.build("8867205331/dockerhub:${env.BUILD_NUMBER}")
	    }

	    stage('Deploy Docker Image'){

	      // deploy docker image to nexus

	      echo "Docker Image Tag Name: ${dockerImageTag}"

		   docker.withRegistry('https://registry.hub.docker.com', 'docker-hub-credentials') {
	          dockerImage.push("${env.BUILD_NUMBER}")
	            dockerImage.push("latest")
	       }

	    }
	}
