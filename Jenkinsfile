pipeline {
     agent any
     environment {
        EMAIL_BODY = 
        """
            <p>EXECUTED: Job <b>\'${env.JOB_NAME}:${env.BUILD_NUMBER})\'</b></p>
            <p>
            View console output at 
            "<a href="${env.BUILD_URL}">${env.JOB_NAME}:${env.BUILD_NUMBER}</a>"
            </p> 
        """
        EMAIL_SUBJECT_SUCCESS = "Status: 'SUCCESS' -Job \'${env.JOB_NAME}:${env.BUILD_NUMBER}\'" 
        EMAIL_SUBJECT_FAILURE = "Status: 'FAILURE' -Job \'${env.JOB_NAME}:${env.BUILD_NUMBER}\'" 
        EMAIL_RECIPIENT = 'zaktales@gmail.com'
    }
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
        stage('Deploy to Heroku') {
            steps {
                withCredentials([usernameColonPassword(credentialsId: 'heroku', variable: 'HEROKU_CREDENTIALS' )]){
                sh 'git push https://${HEROKU_CREDENTIALS}@git.heroku.com/stormy-thicket-98798.git master'
                }
            }
        }
       stage ('Email') {
            steps {
                emailext ( 
                    subject: 'Jenkins Build Status', 
                    body: currentBuild.currentResult + ' : ' + '${env.JOB_NAME} [${env.BUILD_NUMBER}]', 
                    to: 'zaktales@gmail.com')
            }
        } 
        stage ('Slack') {
        steps {
            slackSend botUser: true, channel: 'project', message: 'Message from Jenkins', teamDomain: 'zachariaip1', tokenCredentialId: 'SLACK'
            }
        } 
    }
    post {
        success {
            mail to: EMAIL_RECIPIENT,
            body: EMAIL_BODY, 
            subject: EMAIL_SUBJECT_SUCCESS
        }
        failure {
            mail to: EMAIL_RECIPIENT,
            body: EMAIL_BODY, 
            subject: EMAIL_SUBJECT_FAILURE 
        }
    }
}