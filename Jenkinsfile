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
        success {
            mail to: zaktales@gmail.com, subject: ‘The Pipeline successfully ran the Build :(‘
    }
  }
}