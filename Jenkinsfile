pipeline {
      agent any
   tools{
       maven "M3"
   }
      stages {
        stage('Build') {
          steps {
            echo 'Building...'
                            sh 'mvn clean verify' 
          }
        }
        stage('SNYK') {
          steps {
            echo 'Testing...'
            snykSecurity(
              snykInstallation: "SNYK_LATEST",
              snykTokenId: "SNYKAPI",
              // place other parameters here
            )
          }
        }
        stage('Deploy') {
          steps {
            echo 'Deploying...'
          }
        }
      }
    }
