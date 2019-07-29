node{
     
    stage('SCM Checkout'){
        git credentialsId: 'GIT_HUB', url:  'https://github.com/jaisabhi1/spring-boot-mongo-docker.git',branch: 'master'
    }
    
    stage(" Maven Clean Package"){
        def mvn_version = 'localmaven'
        withEnv( ["PATH+MAVEN=${tool mvn_version}/bin"] ) {
        sh "mvn clean package"
	}
    } 
    
    
    
