node{
    stage ('cloning the code from git') {
        git 'https://github.com/krunalbhoyar/NodeSonarExample.git'
    }

    stage ('sonarqube analysis') {
            sh 'npm install -- save express jest' 
	    sh 'npm install -D sonarqube-scanner jest-sonar-reporter supertest' 
            
	    
	    //def scannerhome = tool 'sonarqube';
        withSonarQubeEnv('sonarqube') {
	    sh 'echo "==========Running Test Cases==========="'
	    sh 'npm run test'
            sh 'echo "==============Scanning code coverage================="'
	    sh 'sudo npm run sonar'
	    
    }
    }
    //stage("Quality gate") {
       //timeout(time: 1, unit: 'HOURS') {
                //waitForQualityGate abortPipeline: true
              //}
	//}
	
	
	
    //stage('OWASP Dependency Check') {
         
          //sh 'rm owasp* || true'
          //sh 'wget "https://raw.githubusercontent.com/krunalbhoyar/NodeSonarExample/master/owasp-dependency-check.sh" '
          //sh 'chmod +x owasp-dependency-check.sh'
          //sh 'sudo chmod 777 odc-reports'
          //sh 'bash owasp-dependency-check.sh'
          //archive (includes: 'odc-reports/*html')

     //}
}

