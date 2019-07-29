node{
       
    
    stages {
	    
	 stage('SCM Checkout'){
        git credentialsId: 'GIT_HUB', url:  'https://github.com/jaisabhi1/spring-boot-mongo-docker.git',branch: 'master'
    }
	    
        stage ('Checking java version') {

            steps {
             
                    sh 'java -version'
         
            }
        }

        stage ('exporting maven Environment variable') {

            steps {
             
                    sh 'export M2_HOME=/opt/maven'
                    sh 'export M2_HOME=/opt/maven'
                
            }
        }


        stage ('maven version') {
            steps {
               
                    sh 'mvn -version'
                
            }
        }

        stage ('Building APP') {
            steps {
               
                    sh 'mvn clean package'
                
            }
        }
    }
}
