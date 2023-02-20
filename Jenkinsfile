pipeline {
     agent { dockerfile true }
        environment {
        HOME = "${env.WORKSPACE}"
    }
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