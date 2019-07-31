node{
     
    stage('SCM Checkout'){
        git credentialsId: 'GIT_HUB', url:  'https://github.com/jaisabhi1/spring-boot-mongo-docker.git/',branch: 'master'
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
        withCredentials([usernamePassword(credentialsId: 'DOCKER_HUB', passwordVariable: 'dockerpassword', usernameVariable: 'dockeruser')]) {
          sh "docker login ${DOCKER_HUB}"
          }
        sh 'docker push jaisabhi1/spring-boot-mongo'
     }
     
     stage("Deploy To Kuberates Cluster"){
       kubernetesDeploy(
         configs: 'springBootMongo.yml', 
         kubeconfigId: 'KUBERNATES_CONFIG',
         enableConfigSubstitution: true
        )
     }
	 
	  /**
      stage("Deploy To Kuberates Cluster"){
        sh 'kubectl apply -f pringBootMongo.yml'
      } **/
     
}
