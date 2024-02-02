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
		//stage('Push artifacts into artifactory') {
                         //steps {
                                 //sh 'curl -fL https://getcli.jfrog.io | sh'
				 //sh 'echo ${ARTIFACTORY_ACCESS_TOKEN}'
                                 //sh './jfrog rt u --url ${JFROG_CLI_BUILD_URL} --access-token ${ARTIFACTORY_ACCESS_TOKEN} ./*.jar  maven-demo/'
                                 //jf 'rt build-publish'
                                 //  sh  './jfrog rt bp  --url https://preethisagar114376.jfrog.io/artifactory --access-token ${ARTIFACTORY_ACCESS_TOKEN} ${JOB_NAME} ${BUILD_NUMBER}'
                                //}
                             //}
		//stage('Static Code Analysis') {
		       //environment {
		             //SONAR_URL = "http://3.109.212.222:9000"
		        //}
		           //steps {
		                 //withCredentials([string(credentialsId: 'sonar', variable: 'SONAR_AUTH_TOKEN')]) {
		                 //sh 'mvn sonar:sonar -Dsonar.login=$SONAR_AUTH_TOKEN -Dsonar.host.url=${SONAR_URL}'
		              //}
		          //}
		      //}

	          stage('Docker Build and Tag') {
		            steps {
			          sh 'docker build -t preethisagar114376.jfrog.io/docker-demo/samplewebapp:${BUILD_NUMBER} --pull=true .'
				  sh 'docker images'
				  //sh 'docker tag samplewebapp docker-demo/samplewebapp:latest'
				  //sh 'docker tag samplewebapp docker-demo/samplewebapp:$BUILD_NUMBER'
			          //sh 'docker tag samplewebapp haripreethisagar/ciproject:latest'
			          //sh 'docker tag samplewebapp haripreethisagar/ciproject:$BUILD_NUMBER'

		               }
	                   }
		//stage('Trivy Scan') {
			 //steps {
				 //sh 'trivy image haripreethisagar/ciproject:$BUILD_NUMBER  --output report.html || true'
		                   //sh 'trivy -h'
                                   //sh 'mkdir -p reports'
                                   //sh 'sudo apt-get -y install tree'
                                   //sh 'trivy image $DOCKER_IMAGE_NAME  --output report.html || true'
                                   //sh 'tree'
                                   //sh 'ls -lrth'
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
		  stage('push image to jfrog artifactory'){
			  steps {
			     script {
				       //sh 'docker login ${ARTIFACTORY_URL} -u admin -p ${ARTIFACTORY_CREDS_ID}'
				       //sh 'docker tag samplewebapp preethisagar114376.jfrog.io/docker-demo/samplewebapp:latest' 
				       //sh 'docker push https://preethisagar114376.jfrog.io/docker-demo/samplewebapp:$BUILD_NUMBER'
			     //}
			  //}
		  //}
                 //stage('Push Image to Artifactory') {
	                 //steps {
			   //rtDockerPush(
			     //serverId: "artifactory",
			     //image: "preethisagar114376.jfrog.io/docker-demo/samplewebapp:${BUILD_NUMBER}",
			     //targetRepo: 'docker-demo')
			 //}
	                //}
			 }
		  // stage('publish build info'){
		         //steps{
		           // rtPublishBuildInfo(
			       // serverId: "artifactory"
			//)
		    // }
		   //}
																									  
					//}
				      //}
				   //}
				//}
			     //}

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
}
}
	}
}

