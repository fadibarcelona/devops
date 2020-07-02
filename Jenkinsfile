pipeline {
   agent { label 'master' }
        stages {
        stage('Checking out Code from Git') {
           
            steps { 
             echo "Checking out Code from Git"
              
            }
        }
           
		 stage('Bulding Image with Custom Changes ') {
           
                steps { 
                    dir ('/root/docker/devops') {
                    sh "docker build -f Dockerfile . -t  ubuntu:$tag"
                    
                    }
            }
            }	        
		
		stage('Checking Existing Container Status ') {
           
                steps { 
                    dir ('/root/docker/') {
                    sh "./checkcontainer.sh"
                    
                    }
            }
            }
            
            stage('Starting New Container ') {
             
                steps { 
                    dir ('/root/docker/devops') {
                    sh "docker run -d --name http -p 8081:80 ubuntu:$tag "
                    
                    }
            }
            }
	}
		
		post {
    always {
	  
      script {
        sh """curl -D- -u "stariq@gbmme.com:mhj7CpOQgGwPJ8SezxnQ1B7D" -X POST --data '{"fields":{"project":{"key": "WEB"},"summary": "Jenkins $BUILD_NUMBER","description": "$JOB_URL ","issuetype": {"name": "Report an incident"}}}' -H "Content-Type: application/json" https://gbmme.atlassian.net//rest/api/2/issue/"""
      }
    }
	}
            
            
        
}
