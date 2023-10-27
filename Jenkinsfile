pipeline {
  agent any

  tools { 
    nodejs "node" // Make sure "node" is the correct tool name for your Node.js installation in Jenkins.
  }

  stages {
    stage('Git') {
      steps {
        git 'https://github.com/ashwin3197/pipeline.git' // Replace with your Git repository URL
      }
    }

    stage('Build') {
      steps {
        sh 'npm install'
        sh 'npm run build' // Build command
      }
    }

    stage('Test') {
      steps {
        sh 'npm test' // Run tests (modify as needed)
      }
    }
  }
}
