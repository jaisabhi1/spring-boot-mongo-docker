node{
     
    stage('SCM Checkout'){
        git credentialsId: 'GIT_CREDENTIALS', url:  'https://github.com/jaisabhi1/spring-boot-mongo-docker.git',branch: 'master'
    }
    
    stage(" Maven Clean Package"){
      def mavenHome =  tool name: "localmaven", type: "maven"
         sh " mvn clean package"
      
    } 
    
    
    stage('Build Docker Image'){
        sh 'docker build -t jaisabhi1/spring-boot-mongo .'
    }
    
    stage('Push Docker Image'){
        withCredentials([string(credentialsId: 'Dockerhub', variable: 'Dockerhub')]) {
          sh "docker login -u jaisabhi1 -p ${Dockerhub}"
        }
        sh 'docker push jaisabhi1/spring-boot-mongo'
     }
     
      stage("Deploy To Kuberates Cluster"){
         withCredentials([string(credentialsId: 'jenkins', variable: 'jenkins')]) {
            kubectl get pods
	 }
     }
	 
	  /**
      stage("Deploy To Kuberates Cluster"){
        sh 'kubectl apply -f pringBootMongo.yml'
      } **/
     
}
