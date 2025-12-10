pipeline {
    agent any

    environment {
        NETLIFY_AUTH_TOKEN = credentials('netlify-token')
        NETLIFY_SITE_ID = credentials('netlify-site-id')
    }

    stages {
        // No need for a Checkout stage if using Pipeline from SCM
        stage('Install Netlify CLI') {
            steps {
                sh '''
                curl -fsSL https://deb.nodesource.com/setup_18.x | bash -
                apt-get install -y nodejs
                npm install -g netlify-cli
                '''
            }
        }

        stage('Deploy to Netlify') {
            steps {
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
