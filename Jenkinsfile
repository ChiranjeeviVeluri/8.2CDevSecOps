pipeline { 
  agent any 
 
  stages { 
    stage('Checkout') { 
      steps { 
        git branch: 'main', url: 'https://github.com/ChiranjeeviVeluri/8.2CDevSecOps.git' 
      } 
    } 
 
    stage('Install Dependencies') { 
      steps { 
        sh 'npm install' 
      } 
    } 
 
    stage('Run Tests') { 
      steps { 
        sh 'npm test || true' // Allows pipeline to continue despite test failures 
      } 
    } 
 
    stage('Generate Coverage Report') { 
      steps { 
        // Ensure coverage report exists 
        sh 'npm run coverage || true' 
      } 
    } 
 
    stage('NPM Audit (Security Scan)') { 
      steps { 
        sh 'npm audit || true' // This will show known CVEs in the output 
      } 
    } 
  stage('SonarCloud Analysis') {
  steps {
    withCredentials([string(credentialsId: 'JenkinsToken', variable: 'SONAR_TOKEN')]) {
      sh '''
        wget https://binaries.sonarsource.com/Distribution/sonar-scanner-cli/sonar-scanner-cli-4.8.0.2856-linux.zip
        unzip sonar-scanner-cli-4.8.0.2856-linux.zip
        export PATH=$PATH:$PWD/sonar-scanner-4.8.0.2856-linux/bin
        sonar-scanner
      '''
    }
  }
}

 
  } 
}
