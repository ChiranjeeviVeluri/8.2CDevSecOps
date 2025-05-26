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
        # Download SonarScanner CLI
        curl -O https://binaries.sonarsource.com/Distribution/sonar-scanner-cli/sonar-scanner-cli-4.8.0.2856-linux.zip

        # Extract the archive
        unzip -o sonar-scanner-cli-4.8.0.2856-linux.zip

        # Run SonarScanner
        ./sonar-scanner-4.8.0.2856-linux/bin/sonar-scanner \
          -Dsonar.projectKey=ChiranjeeviVeluri_8-2CDevSecOps \
          -Dsonar.organization=chiranjeeviveluri \
          -Dsonar.sources=. \
          -Dsonar.host.url=https://sonarcloud.io \
          -Dsonar.login=$SONAR_TOKEN
      '''
    }
  }
}
 
  } 
}
