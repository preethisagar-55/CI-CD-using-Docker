pipeline {
	agent any
	tools {
		maven "maven 3.6.3"
	}
	environment {
	    SONAR_AUTH_TOKEN = credentials('sonar')
	    ARTIFACTORY_CREDS_ID='jfrogtoken'
	    //env.USERNAME = 'USERNAME'
	    //env.PASSWORD = 'PASSWORD'
	    ARTIFACTORY_URL = 'preethisagar114376.jfrog.io'
	    DOCKER_IMAGE_NAME= 'samplewebapp'
	    DOCKER_TAG = 'latest'
	    DOCKER_REPO = 'dockerdemo' 
        }
	stages {
		stage('checkout') {
			steps {

				git branch: 'master', credentialsId: 'git', url: 'https://github.com/preethisagar-55/CI-CD-using-Docker.git'

			}
		}

		stage('Execute Maven') {
			steps {

				sh 'mvn package'
			}
		}
		//stage('Push artifacts into artifactory') {
                         //steps {
                                 //sh 'curl -fL https://getcli.jfrog.io | sh'
				 //sh 'echo ${ARTIFACTORY_ACCESS_TOKEN}'
                                 //sh './jfrog rt u --url ${JFROG_CLI_BUILD_URL} --access-token ${ARTIFACTORY_ACCESS_TOKEN} ./*.jar  maven-demo/'
                                 //jf 'rt build-publish'
                                 //  sh  './jfrog rt bp  --url https://preethisagar114376.jfrog.io/artifactory --access-token ${ARTIFACTORY_ACCESS_TOKEN} ${JOB_NAME} ${BUILD_NUMBER}'
                                //}
                             //}
		stage('Static Code Analysis') {
		  environment {
		    SONAR_URL = "http://3.109.212.222:9000"
		  }
		        steps {
		                 withCredentials([string(credentialsId: 'sonar', variable: 'SONAR_AUTH_TOKEN')]) {
		                 sh 'mvn sonar:sonar -Dsonar.login=$SONAR_AUTH_TOKEN -Dsonar.host.url=${SONAR_URL}'
		              }
		          }
		      }

	        stage('Docker Build and Tag') {
		         steps {
			          sh 'docker build -t samplewebapp:latest .'
			          sh 'docker tag samplewebapp haripreethisagar/ciproject:latest'
			          sh 'docker tag samplewebapp haripreethisagar/ciproject:$BUILD_NUMBER'

		               }
	                   }
		//stage('Trivy Scan') {
			 //steps {
				 //sh 'trivy image haripreethisagar/ciproject:$BUILD_NUMBER  --output report.html || true'
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
		  stage('push docker image to artifactory'){
                            steps{
				script{
					 withCredentials([usernamePassword(credentialsId:"${ARTIFACTORY_CREDS_ID}")]){
					 //env.USERNAME = USERNAME
					 //env.PASSWORD = PASSWORD
					 env.ARTIFACTORY_URL = ARTIFACTORY_URL
					 env.DOCKER_IMAGE_NAME = DOCKER_IMAGE_NAME
					 env.DOCKER_TAG = DOCKER_TAG
					 env.DOCKER_REPO = DOCKER_REPO
					 sh "jfrog rt config --url $ARTIFACTORY_URL --access-token $ARTIFACTORY_CREDS_ID"
					 sh "jfrog rt $DOCKER_IMAGE_NAME:$DOCKER_TAG $DOCKER_REPO"
				      }
				}
			}
		}
	}
}

//stage('Run Docker container on Jenkins Agent') {

// steps 
//{
//  sh "docker run -d -p 8003:8080 nikhilnidhi/samplewebapp"

//}
//  }
//stage('Run Docker container on remote hosts') {

//steps {
//sh "docker -H ssh://jenkins@172.31.28.25 run -d -p 8003:8080 nikhilnidhi/samplewebapp"

// }
//}
// }
//}
 



	

