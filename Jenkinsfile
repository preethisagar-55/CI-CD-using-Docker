pipeline {
	agent any
	tools {
		maven "maven 3.6.3"
	}
	environment {
	    ARTIFACTORY_ACCESS_TOKEN = credentials('jfrog')
	    SONAR_AUTH_TOKEN = credentials('sonar')
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
		stage('Push artifacts into artifactory') {
                         //steps {
                                 //sh 'curl -fL https://getcli.jfrog.io | sh'
                                 sh './jfrog rt u --url https://preethisagar114376.jfrog.io/artifactory --access-token ${ARTIFACTORY_ACCESS_TOKEN} ./*.jar  demo-release/'
                                 jf 'rt build-publish'
                                 //  sh  './jfrog rt bp  --url https://preethisagar114376.jfrog.io/artifactory --access-token ${ARTIFACTORY_ACCESS_TOKEN} ${JOB_NAME} ${BUILD_NUMBER}'
                                }
                             }
		//stage ('SonarQube analysis') {
                    //steps {
                        //withSonarQubeEnv('sonar') {
                        //sh 'mvn sonar:sonar'
                        //}
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

                 stage('Publish image to Docker Hub') {
                          steps {
                                    withDockerRegistry([ credentialsId: "docker", url: "" ]) {
                                    sh  'docker push haripreethisagar/ciproject:latest'
                                    sh  'docker push haripreethisagar/ciproject:$BUILD_NUMBER' 
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
 }
}
}

