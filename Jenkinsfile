pipeline {
  agent any

  stages {
    stage('download image') {
      steps {
         sh '''#!/bin/bash
                 curl -O https://cloud-images.ubuntu.com/releases/focal/release/ubuntu-20.04-server-cloudimg-amd64.img
         '''
    archiveArtifacts artifacts: 'ubuntu-20.04-server-cloudimg-amd64.img', followSymlinks: false
    }
  
}
  }
}
