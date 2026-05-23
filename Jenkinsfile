pipeline {
    agent {label "Frontend"}
    environment {

        APP_SERVER = "172.31.38.77"
        DEPLOY_DIR = "/var/www/html"
    }
   stages{
      stage('Pre Build Actions') {
            steps{
                sh 'npm install'            
            }
        }        
        stage('Build') {
            steps{
                sh 'npm run build'
            }
        }
        stage('Post Build Actions') {
          steps {
                sh """
                echo 'Cleaning old files on app server'
                ssh jenkins@${APP_SERVER} 'rm -rf ${DEPLOY_DIR}/*'
                echo 'Copying frontend build'
                scp -r dist/* jenkins@${APP_SERVER}:${DEPLOY_DIR}/
                echo 'Restarting nginx'
                ssh jenkins@${APP_SERVER} 'sudo systemctl restart nginx'
                """
            }
        }
    }
}      
