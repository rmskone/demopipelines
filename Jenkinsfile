pipeline {
    agent any

  stages {
    stage('download image') {
      steps {
         sh '''#!/bin/bash
                 curl -O https://cloud-images.ubuntu.com/releases/focal/release/ubuntu-20.04-server-cloudimg-amd64.img
         '''
//    archiveArtifacts artifacts: 'ubuntu-20.04-server-cloudimg-amd64.img', followSymlinks: false
    }
  
}
        stage ('Upload') {
            steps {
                rtUpload (
                    // Obtain an Artifactory server instance, defined in Jenkins --> Manage Jenkins --> Configure System:
                    serverId: "rmskone1_art",
                    spec: """{
                            "files": [
                                    {
                                        "pattern": "ubuntu-20.04-server-cloudimg-amd64.img",
                                        "target": "default-generic-local",
                                        "props": "p1=v1;p2=v2"
                                     }
                                ]
                            }"""
                )
            }
        }

        stage ('Set Props') {
            steps {
                rtSetProps (
                    serverId: "rmskone1_art",
                    spec: """{
                           "files": [
                            {
                                "pattern": "default-generic-local/*(Pipeline).zip",
                                "props": "p1=v1;p2=v2"
                              }
                           ]
                          }""",
                    props: "p3=v3",
                    failNoOp: true
                )
            }
        }

        stage ('Download') {
            steps {
                rtDownload (
                    serverId: "rmskone1_art",
                    spec: """{
                            "files": [
                                    {
                                        "pattern": "default-generic-local/*(Pipeline).zip",
                                        "target": "Bazinga/{1}/",
                                        "props": "p1=v1;p2=v2"
                                    }
                                ]
                            }"""
                )
            }
        }

        stage ('Publish build info') {
            steps {
                rtPublishBuildInfo (
                    serverId: "rmskone1_art"
                )
            }
        }

        stage ('Delete Props') {
            steps {
                rtDeleteProps (
                    serverId: "rmskone1_art",
                    spec: """{
                               "files": [
                                {
                                    "pattern": "default-generic-local/*(Pipeline).zip",
                                    "props": "p3=v3"
                                  }
                               ]
                              }""",
                    props: "p1,p2",
                    failNoOp: true
                )
            }
        }
    }
}
