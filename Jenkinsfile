pipeline {
    agent none
        stages {
        stage('Checking out Code from Git') {
            agent { label 'master' }
            steps { 
             echo "Checking out Code from Git"
              
            }
        }
           
		 stage('Bulding Image with Custom Changes ') {
            agent { label 'master' }
                steps { 
                    dir ('/root/docker/devops') {
                    sh "docker build -f Dockerfile . -t  ubuntu:$tag"
                    
                    }
            }
            }	        
		
		stage('Removing Old container ') {
            agent { label 'master' }
                steps { 
                    dir ('/root/docker/devops') {
                    sh "docker stop http && docker rm http"
                    
                    }
            }
            }
            
            stage('Starting New Container ') {
            agent { label 'master' }
                steps { 
                    dir ('/root/docker/devops') {
                    sh "docker run -d --name http -p 8081:80 ubuntu:$tag http "
                    
                    }
            }
            }
            
            
        }
}
