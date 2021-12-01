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
                   sh "${scannerHome}/bin/sonar-scanner -Dsonar.projectKey=OWASP -Dsonar.sources=. -Dsonar.host.url=http://172.18.0.3:9000 -Dsonar.login=9eced86a02272015196b22804b2c9c22bbd66bc8" 
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

