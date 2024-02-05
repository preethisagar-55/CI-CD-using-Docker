pipeline {
	agent any
	tools {
		maven "maven 3.6.3"
		jfrog "jfrogcli"
	}
	environment {
	    SONAR_AUTH_TOKEN = credentials('sonar')
	    ARTIFACTORY_CREDS_ID='jfrogtoken'
	    //API_KEY = credentials('jfrogAPI')
	    REPO_NAME = 'dockerdemo'
	    ARTIFACT_PATH = 'docker-demo/samplewebapp'
	    ARTIFACT_FILE = 'samplewebapp'
	    //env.USERNAME = 'USERNAME'
	    //env.PASSWORD = 'PASSWORD'
	    ARTIFACTORY_URL = 'https://preethisagar114376.jfrog.io'
	    DOCKER_IMAGE_NAME= 'preethisagar114376.jfrog.io/docker-demo/samplewebapp:${BUILD_NUMBER}'
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
		
		

	    stage('Docker Build and Tag') {
		    steps {
			          //sh 'docker build -t preethisagar114376.jfrog.io/docker-demo/samplewebapp:${BUILD_NUMBER} --pull=true .'
				  //sh 'docker images'
				  //sh 'docker tag samplewebapp docker-demo/samplewebapp:latest'
				  //sh 'docker tag samplewebapp docker-demo/samplewebapp:$BUILD_NUMBER'
			          sh 'docker tag samplewebapp haripreethisagar/ciproject:latest'
			          sh 'docker tag samplewebapp haripreethisagar/ciproject:$BUILD_NUMBER'
				      sh 'docker build -t samplewebapp haripreethisagar/ciproject:$BUILD_NUMBER .'
			    }
                             }
	                   }
		

        stage('Publish image to Docker Hub') {
            steps {
                        withDockerRegistry([ credentialsId: "docker", url: "" ]) {
                        sh  'docker push haripreethisagar/ciproject:latest'
                        sh  'docker push haripreethisagar/ciproject:$BUILD_NUMBER' 
                                }
                             }
		       }  
		  
                 
        stage('Run Docker container on Jenkins Agent') {
            steps{
                    sh "docker run -d -p 8003:8080 samplewebapp:${BUILD_NUMBER}"

                  }
                   }

                    }


