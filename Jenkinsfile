node{
    stage ('cloning the code from git') {
        git 'https://github.com/krunalbhoyar/NodeSonarExample.git'
    }

    stage ('sonarqube analysis') {
            sh 'npm install -- save express jest' 
	    sh 'npm install -D sonarqube-scanner jest-sonar-reporter supertest' 
            
	    
	    //def scannerhome = tool 'sonarqube';
        withSonarQubeEnv('sonarqube') {
	    sh 'npm -s run test'
	    sh 'sudo npm run sonar'
            //sh 'npm run test'
            //sh "${scannerhome}/bin/sonar-scanner \
            //-D sonar.login=admin\
            //-D sonar.password=admin \
	    //-D sonar.projectKey=NodeSonarExample \
	    //-D sonar.sources=src "
	    
    }
     
	
def tries = 0
  sonarResultStatus = "PENDING"
  while ((sonarResultStatus == "PENDING" || sonarResultStatus == "IN_PROGRESS") && tries++ < 5) {
      try {
          sonarResult = waitForQualityGate abortPipeline: true
          sonarResultStatus = sonarResult.status
      } catch(ex) {
          echo "caught exception ${ex}"
      }
      echo "waitForQualityGate status is ${sonarResultStatus} (tries=${tries})"
  }
  if (sonarResultStatus != 'OK') {
      error "Quality gate failure for SonarQube: ${sonarResultStatus}"
  }

    }

	
    stage('OWASP Dependency Check') {
         
          sh 'rm owasp* || true'
          sh 'wget "https://raw.githubusercontent.com/krunalbhoyar/sonarqubetest/master/owasp-dependency-check.sh" '
          sh 'chmod +x owasp-dependency-check.sh'
         // sh 'sudo chmod 777 odc-reports'
          sh 'bash owasp-dependency-check.sh'
     }
}
