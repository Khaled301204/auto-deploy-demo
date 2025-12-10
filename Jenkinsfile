pipeline {
    // Use a Node.js Docker image with Node pre-installed
    agent {
        docker {
            image 'node:20-bullseye' 
        }
    }

    environment {
        // Make sure these credentials exist in Jenkins
        NETLIFY_AUTH_TOKEN = credentials('netlify-token')
        NETLIFY_SITE_ID = credentials('netlify-site-id')
    }

    stages {
        stage('Checkout') {
            steps {
                // Repo is already checked out by Pipeline from SCM
                echo "Repo already checked out to workspace."
            }
        }

        stage('Install Netlify CLI') {
            steps {
                sh 'npm install -g netlify-cli'
            }
        }

        stage('Deploy to Netlify') {
            steps {
                // Deploy the static site
                sh 'netlify deploy --dir=. --prod'
            }
        }
    }

    post {
        success {
            echo '✅ Deployment Successful!'
        }
        failure {
            echo '❌ Deployment Failed!'
        }
    }
}
