node{
     
    stage('SCM Checkout'){
        git credentialsId: 'GIT_CREDENTIALS', url:  'https://github.com/jaisabhi1/spring-boot-mongo-docker.git',branch: 'master'
    }
    
    stage(" Maven Clean Package"){
      def mavenHome =  tool name: "localmaven", type: "maven"
      def mavenCMD = "${mavenHome}/bin/mvn"
      sh "${mavenCMD} clean package"
      
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
       withCredentials([kubeconfigContent(credentialsId: 'Kubeconfig', variable: 'KUBECONFIG_CONTENT')]) {
        sh '''cat "$KUBECONFIG_CONTENT" >kubeconfig && kubectl version --kubeconfig kubeconfig && rm kubeconfig'''
}
     }
	 
	  /**
      stage("Deploy To Kuberates Cluster"){
        sh 'kubectl apply -f pringBootMongo.yml'
      } **/
     
}
