node{
     
    stage('SCM Checkout'){
        git credentialsId: 'GIT_HUB', url:  'https://github.com/gsr916/spring-boot-mongo-docker.git',branch: 'master'
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
       kubernetesDeploy(
         configs: 'springBootMongo.yml', 
         kubeconfigId: 'Kubeconfig',
         enableConfigSubstitution: true
        )
     }
     
}
