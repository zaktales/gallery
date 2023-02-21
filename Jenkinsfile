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
        stage('Tests') {
            steps {
                sh 'npm install mocha chai --save-dev'
                sh 'npm test'
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
       stage ('Email') {
        steps {
            emailext attachLog: true, body: 'Jenkins Build Status', subject: 'Jenkins Build Status', to: 'zaktales@gmail.com'
            }
        } 
        stage ('Slack') {
        steps {
            slackSend botUser: true, channel: 'project', message: 'Message from Jenkins', teamDomain: 'zachariaip1', tokenCredentialId: 'SLACK'
            }
        } 
    }
}