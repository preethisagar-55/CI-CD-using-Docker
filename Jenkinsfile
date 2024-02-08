pipeline {
	agent any
	tools {
		maven "maven 3.6.3"
		jfrog "jfrogcli"
	}
	environment {
	    SONAR_AUTH_TOKEN = credentials('sonar')
	    //ARTIFACTORY_CREDS_ID='jfrogtoken'
	    //API_KEY = credentials('jfrogAPI')
	    REPO_NAME = 'dockerdemo'
	    ARTIFACT_PATH = 'docker-demo/samplewebapp'
	    ARTIFACT_FILE = 'samplewebapp'
	    //env.USERNAME = 'USERNAME'
	    //env.PASSWORD = 'PASSWORD'
	    //ARTIFACTORY_URL = 'https://preethisagar114376.jfrog.io'
	    DOCKER_IMAGE_NAME= 'haripreethisagar/ciproject:$BUILD_NUMBER'
	    DOCKER_TAG = 'latest'
	    DOCKER_REPO = 'dockerdemo' 
        }
	stages {
		stage('checkout') {
			steps {
                                timeout(time:10,unit:'MINUTES'){
				git branch: 'master', credentialsId: 'git', url: 'https://github.com/preethisagar-55/CI-CD-using-Docker.git'
				}
                           }
		}

		stage('Execute Maven') {
			steps {

				sh 'mvn package'
			}
		}
		//stage('Static Code Analysis') {
		  //environment {
		    //SONAR_URL = "http://3.109.212.222:9000"
		  //}
		        //steps {
		                 //withCredentials([string(credentialsId: 'sonar', variable: 'SONAR_AUTH_TOKEN')]) {
		                 //sh 'mvn sonar:sonar -Dsonar.login=$SONAR_AUTH_TOKEN -Dsonar.host.url=${SONAR_URL}'
		              //}
		          //}
		     // }
		//stage('upload maven artifact to jfrog') {
	                 //steps {
			   //rtUpload(
			     //serverId: "artifactory",
			     //spec: '''{
	                       //"files": [
			         //{
	                           //"pattern": "*.war",
			           //"target" : "maven-demo/"
	                         //}
			       //]
	                      //}''',
			     //)
			   //}
			 //}
		
		

	         stage('Docker Build and Tag') {
		         steps {
			          sh 'docker build -t preethisagar114376.jfrog.io/docker-demo/samplewebapp:${BUILD_NUMBER} --pull=true .'
				  sh 'docker images'
				  //sh 'docker tag samplewebapp docker-demo/samplewebapp:latest'
				  //sh 'docker tag samplewebapp docker-demo/samplewebapp:$BUILD_NUMBER'
			          //sh 'docker build -t samplewebapp:$BUILD_NUMBER .'
			          //sh 'docker tag samplewebapp haripreethisagar/ciproject:latest'
			          //sh 'docker tag samplewebapp haripreethisagar/ciproject:$BUILD_NUMBER'
				     
			    }
                             }
		 //stage('Trivy Scan') {
			  //steps {
				 //sh 'trivy image haripreethisagar/ciproject:$BUILD_NUMBER'
		                 
			 //}
		     //}
		  
	                   
		

                  //stage('Publish image to Docker Hub') {
                         //steps {
                        //withDockerRegistry([ credentialsId: "docker", url: "" ]) {
                        //sh  'docker push haripreethisagar/ciproject:latest'
                        //sh  'docker push haripreethisagar/ciproject:$BUILD_NUMBER' 
                                //}
                             //}
		       //}  
		  
                 
        //stage('Run Docker container on Jenkins Agent') {
            //steps{
                    //sh "docker run -d -p 8003:8080 samplewebapp:${BUILD_NUMBER}"

                  //}
                   //}
	stage('Push Image to Artifactory') {
	                 steps {
			   rtDockerPush(
			     serverId: "artifactory",
			     image: "preethisagar114376.jfrog.io/docker-demo/samplewebapp:${BUILD_NUMBER}",
			     targetRepo: 'docker-demo')
			 }
	                }

                    }
}


