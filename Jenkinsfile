node{
    stage ('cloning the code from git') {
        git 'https://github.com/krunalbhoyar/NodeSonarExample.git'
    }

    stage ('sonarqube analysis') {
            sh 'npm install -- save express jest' 
	    sh 'npm install -D sonarqube-scanner jest-sonar-reporter supertest' 
            sh 'npm run test'
	    sh 'sudo npm run sonar'
    }
    stage('Quality Gates'){
      
     timeout(time: 1, unit: 'HOURS') {
    def qg = waitForQualityGate() 
    if (qg.status != 'OK') {
      error "Pipeline aborted due to quality gate failure: ${qg.status}"
    }
  }
      
  }
	
	
	
   // stage('OWASP Dependency Check') {
         
     //     sh 'rm owasp* || true'
       //   sh 'wget "https://raw.githubusercontent.com/krunalbhoyar/sonarqubetest/master/owasp-dependency-check.sh" '
         // sh 'chmod +x owasp-dependency-check.sh'
         // sh 'sudo chmod 777 odc-reports'
         // sh 'bash owasp-dependency-check.sh'
     //}
}
