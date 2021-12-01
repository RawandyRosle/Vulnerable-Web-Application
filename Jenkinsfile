pipeline { 
    agent any 
    stages { 
        stage ('Checkout') { 
            steps { 
                git branch:'master', url: 'https://github.com/RawandyRosle/Vulnerable-Web-Application.git' 
            } 
        } 
         
        stage('Code Quality Check via SonarQube') { 
           steps { 
               script { 
                def scannerHome = tool 'SonarQube'; 
                   withSonarQubeEnv('SonarQube') { 
                   sh "${scannerHome}/bin/sonar-scanner -Dsonar.projectKey=OWASP -Dsonar.sources=. -Dsonar.host.url=http://172.18.0.2:9000 -Dsonar.login=0d66c4deca5e82214bfbba2b3e9966ed874dc700" 
                   } 
               } 
           } 
        } 
    } 
    post { 
        always { 
            recordIssues enabledForFailure: true, tool: sonarQube() 
        } 
    } 
} 

