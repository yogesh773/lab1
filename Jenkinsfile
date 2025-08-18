pipeline {
    agent any

    stages {
        stage('Deploy from Git to Nginx') {
            steps {
                echo "🚀 Deploying templatemo_594_nexus_flow.zip from Git to Nginx..."
                sh '''
                    set -e
                    git clone https://github.com/yogesh773/webtest.git temp_repo

                    if [ ! -f temp_repo/templatemo_594_nexus_flow.zip ]; then
                        echo "❌ templatemo_594_nexus_flow.zip not found in Git repo!"
                        rm -rf temp_repo
                        exit 1
                    fi

                    echo "📂 Unzipping project..."
                    unzip -o temp_repo/templatemo_594_nexus_flow.zip -d project

                    echo "🗑️ Cleaning old files..."
                    sudo rm -rf /var/www/html/*

                    echo "📥 Copying new files..."
                    sudo cp -r project/* /var/www/html/

                    echo "🔄 Restarting Nginx..."
                    sudo systemctl restart nginx

                    rm -rf temp_repo
                '''
            }
        }
    }

    post {
        failure {
            echo "❌ Deployment failed!"
        }
        success {
            echo "✅ Deployment successful!"
        }
        always {
            echo "🧹 Cleaning up workspace..."
            cleanWs()
        }
    }
}
