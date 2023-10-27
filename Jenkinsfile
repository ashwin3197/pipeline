pipeline {
    agent any

    stages {
        stage('Debug') {
            steps {
                script {
                    echo 'Starting pipeline'

                    try {
                        // Check out your source code from a Git repository
                        checkout scm

                        // Set up Node.js environment
                        def nodeJSHome = tool name: 'NodeJS 16', type: 'NodeJS'
                        env.PATH = "${nodeJSHome}/bin:${env.PATH}"

                        // Build a Docker image for your Node.js application
                        sh 'docker build -t my-node-app:latest .'

                        // Run a Docker container based on the image
                        sh 'docker run -d --name my-node-app-container -p 8080:8080 my-node-app:latest'

                        // Wait for the Node.js app to start
                        sleep time: 30, unit: 'SECONDS'

                        // Test your application (e.g., using curl)
                        sh 'curl -s http://localhost:8080'

                    } catch (Exception e) {
                        echo "Error: ${e.message}"
                        currentBuild.result = 'FAILURE'
                        error("Pipeline failed")
                    }
                }
            }
        }
    }

    post {
        failure {
            echo "Pipeline failed"
            // Additional failure actions
        }
        success {
            echo "Pipeline succeeded"
            // Additional success actions
        }
    }
}
