pipeline {
     agent any
        tools {
            nodejs "NODEJS"
            }
     stages { 
        stage('clone repository') {
            steps { 
                git 'https://github.com/zaktales/gallery'
            }
        }
        stage('Build') {
            steps {
                sh 'npm install'
            }
        }
         stage('Deploy to Heroku') {
            steps {
                withCredentials([usernameColonPassword(credentialsId: 'heroku', variable: 'HEROKU_CREDENTIALS' )]){
                sh 'git push https://${HEROKU_CREDENTIALS}@git.heroku.com/stormy-thicket-98798.git master'
                }
            }
        }
        
     }
     post {
        failure {
            emailext body: 'Check console output at $BUILD_URL to view the results. \n\n ${CHANGES} \n\n -------------------------------------------------- \n${BUILD_LOG, maxLines=100, escapeHtml=false}', 
                    to: "${EMAIL_TO}", 
                    subject: 'Build failed in Jenkins: $PROJECT_NAME - #$BUILD_NUMBER'
        }
        changed {
            emailext body: 'Check console output at $BUILD_URL to view the results.', 
                    to: "${EMAIL_TO}", 
                    subject: 'Jenkins build is back to normal: $PROJECT_NAME - #$BUILD_NUMBER'
        }
     }
}