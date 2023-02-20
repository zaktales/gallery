pipeline {
     agent any
     stages { 
        stage('clone repository') {
            steps { 
                git 'https://github.com/zaktales/gallery'
            }
        }
     }
     stages {
        stage('Build') { 
            steps {
                sh 'npm install' 
            }
        }
    }
}