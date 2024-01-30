pipeline {
    agent any
   tools
    {
       maven "maven 3.6.3"
    }
 stages {
      stage('checkout') {
           steps {
             
                git branch: 'master',credentialsId:'git',url: 'https://github.com/preethisagar-55/CI-CD-using-Docker.git'
             
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
     // }
   }
    
	 
  stage('Docker Build and Tag') {
           steps {
              
                sh 'docker build -t samplewebapp:latest .' 
                sh 'docker tag samplewebapp preethi/samplewebapp:latest'
                sh 'docker tag samplewebapp preethi/samplewebapp:$BUILD_NUMBER'
               
          }
        }
     
  //stage('Publish image to Docker Hub') {
          
           // steps {
        //withDockerRegistry([ credentialsId: "dockerHub", url: "" ]) {
          //sh  'docker push nikhilnidhi/samplewebapp:latest'
        //  sh  'docker push nikhilnidhi/samplewebapp:$BUILD_NUMBER' 
       // }
                  
         // }
      //  }
     
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

