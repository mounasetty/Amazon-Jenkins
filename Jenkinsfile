pipeline {
    agent any

    stages {
        stage('Checkout') {
            steps {
                // Checkout the feature branch
                 git branch: 'main-1.0', url: 'https://github.com/mounasetty/Amazon-Jenkins.git'
            }
        }

        stage('Build and Test') {
            steps {
                // Build the project
                sh 'mvn clean install'
                
                // Run tests
                sh 'mvn test'
            }
        }

        stage('Merge to Main') {
            steps {
                // Check if tests passed
                script {
                    def testsPassed = sh script: 'mvn test', returnStatus: true
                    if (testsPassed == 0) {
                        // Checkout main branch
                        sh 'git checkout main'
                        
                        // Merge main-1.0 branch into main
  sh 'git merge main-1.0'
                        
                        // Push changes to origin
                        sh 'git push origin main'
                    } else {
                        error('Tests failed on the feature branch, merge aborted.')
                    }
                }
            }
        }
    }
}
