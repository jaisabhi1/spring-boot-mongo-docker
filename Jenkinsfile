node{
     
    stage('SCM Checkout'){
        git credentialsId: 'GIT_HUB', url:  'https://github.com/jaisabhi1/spring-boot-mongo-docker.git',branch: 'master'
    }
    
    stage(" Maven Clean Package"){
            def mvn_version = 'localmaven'
	    withEnv( ["PATH+MAVEN=${tool mvn_version}/bin"] ){
            sh "mvn clean package"
	    }
    } 
    
    
    stage('Build Docker Image'){
        sh 'docker build -t dockerhandson/spring-boot-mongo .'
    }
    
    stage('Push Docker Image'){
        withCredentials([string(credentialsId: 'DOKCER_HUB', variable: 'DOKCER_HUB')]) {
          sh "docker login -u dockerhandson -p ${DOKCER_HUB}"
        }
        sh 'docker push dockerhandson/spring-boot-mongo'
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


