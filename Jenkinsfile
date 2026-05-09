pipeline {
    agent any
    stages{
        stage('Pre Build Actions') {
            steps{
                sh 'npm install'
                sh 'sudo systemctl status nginx || sudo apt install nginx -y'
                sh 'sudo systemctl start nginx'            
                        
            }
        }        
        stage('Build') {
            steps{
                sh 'npm run build'
            }
        }
        stage('Post Build ACtions') {
            steps{
                sh 'echo "build completed successfully"'
                sh 'sudo cp -r dist/* /var/www/html/'
                sh 'sudo systemctl restart nginx'
            }
        }
    }
}      
