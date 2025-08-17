pipeline {
    agent any

    stages {
        stage('Checkout') {
            steps {
                echo "📥 Cloning project from GitHub..."
                git branch: 'yogi', url: 'https://github.com/yogesh773/webtest.git'
            }
        }

        stage('Unzip Project') {
            steps {
                echo "📂 Unzipping mywebpage.zip..."
                sh '''
                    rm -rf project
                    mkdir project
                    unzip -o mywebpage.zip -d project
                '''
            }
        }

        stage('Deploy to Nginx') {
            steps {
                echo "🚀 Deploying project to Nginx..."
                sh '''
                    sudo rm -rf /var/www/html/*
                    sudo cp -r project/* /var/www/html/
                '''
            }
        }
    }

    post {
        success {
            echo "✅ Deployment successful! Visit your server IP in browser."
        }
        failure {
            echo "❌ Deployment failed!"
        }
    }
}

