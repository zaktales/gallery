pipeline {
     agent any { dockerfile true }
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
        stage('Build') { 
            steps {
                sh 'npm install' 
            }
        }
}