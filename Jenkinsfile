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
        stage('Tests') {
            steps { 
                sh 'npm run int-test'
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
}