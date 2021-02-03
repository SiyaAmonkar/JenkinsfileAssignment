
pipeline {
    agent any
    environment {
        uuid = UUID.randomUUID().toString()
        registryCredential ='docker'
	    containerName = "shraddhal/seleniumtest2"
        container_version = "1.0.0.${BUILD_ID}"
        dockerTag = "${containerName}:${container_version}"
    }

    tools {
        // Install the Maven version configured as "M3" and add it to the path.
        maven "maven"
    }

    stages {
        stage('Clone Repo and build maven project') {
            steps {
                // Get code from a GitHub repository
                git ' https://github.com/SiyaAmonkar/JenkinsfileAssignment.git'

                // Run Maven on a Unix agent.
               sh '''cd musicstore
                mvn clean package'''

               
            }
}

        stage('Dockerized Tomcat') {
		
		steps {
                	script{
			 	dockerImage = docker.build("shivani221/tomcatcontainer")
			 	docker.withRegistry( '', registryCredential ) {
                        	 dockerImage.push("$BUILD_NUMBER")
                         	dockerImage.push('latest')
				sh 'docker run -d --name tomcatcontainer -p 9090:8080 shivani221/tomcatcontainer:latest'
			 }
			}
                      }
		}
			
			
			
           }
	
         
         }
	    
