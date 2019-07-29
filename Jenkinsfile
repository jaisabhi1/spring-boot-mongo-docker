node{
     
    stage('SCM Checkout'){
        git credentialsId: 'GIT_HUB', url:  'https://github.com/jaisabhi1/spring-boot-mongo-docker.git',branch: 'master'
    }
    
    stage(" Maven Clean Package"){
        sh 'mvn clean package'
	    } 
}
