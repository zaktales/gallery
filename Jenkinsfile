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
     }
        stage('Build') { 
            steps {
                sh 'npm install' 
            }
        }
}