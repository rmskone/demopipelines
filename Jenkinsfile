
  stages {
        stage ('Download') {
            steps {
                rtDownload (
                    serverId: "rmskone1_art",
                    spec: """{
                            "files": [
                                    {
                                        "pattern":"*.img",
                                        "target": "default-generic-local"
                                    }
                                ]
                            }"""
                )
            }
        }
    }
}
