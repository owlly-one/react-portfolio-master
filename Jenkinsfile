pipeline {
  agent any

  stages {
    stage('Build and Deploy') {
      steps {
        echo "Building and deploying stages..."
        script {
          // Use 'nvm' to manage Node.js versions
          def nodejsInstallation = tool name: 'nodejs', type: 'jenkins.plugins.nodejs.tools.NodeJSInstallation'
          env.PATH = "${nodejsInstallation}/bin:${env.PATH}"

          // Install dependencies and build
          sh 'yarn install'

          // Run tests (optional)
          // sh 'npm test' // Uncomment if you want to run tests

          // Build and start the application
          sh 'yarn run build'
        }
      }
    }

stage('FTP Upload') {
    steps {
        script {
            ftpPublisher(
                alwaysPublishFromMaster: false,
                continueOnError: true,
                failOnError: true,
                masterNodeName: '',
                publishers: [
                    [ 
                        configName: 'ftpserver', 
                        transfers: [
                            [
                                asciiMode: false,
                                cleanRemote: true,
                                excludes: '',
                                flatten: false,
                                makeEmptyDirs: false, 
                                noDefaultExcludes: false, 
                                patternSeparator: '[, ]+', 
                                remoteDirectory: '/', 
                                remoteDirectorySDF: false, 
                                removePrefix: 'build', 
                                sourceFiles: 'build/**'
                            ]
                        ]
                    ] 
                ]
            )
        }
    }
}

}
    }

