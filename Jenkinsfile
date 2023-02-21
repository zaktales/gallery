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
        stage('Ok') {
            steps {
                echo "OK"
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
        always {
            emailext body: 'Email from Jenkins', recipientProviders: [[$class: 'DevelopersRecipientProvider'], [$class: 'RequesterRecipientProvider']], subject: 'Test Subject', to: 'zaktales@gmail.com'
        }
    }
}