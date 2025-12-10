pipeline {
    agent any

    environment {
        NETLIFY_AUTH_TOKEN = credentials('netlify-token')
        NETLIFY_SITE_ID = credentials('netlify-site-id')
    }

    stages {
        stage('Checkout') {
            steps {
                // Clone the public repo
                sh 'git clone https://github.com/Khaled301204/auto-deploy-demo.git .'
            }
        }

        stage('Install Netlify CLI') {
            steps {
                // Install Node.js & Netlify CLI
                sh '''
                curl -fsSL https://deb.nodesource.com/setup_18.x | bash -
                apt-get install -y nodejs
                npm install -g netlify-cli
                '''
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
