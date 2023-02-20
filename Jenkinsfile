pipeline {
     agent any
     tools { 
        gradle "Gradle-6"
        }
     stages { 
        stage('clone repository') {
            steps { 
                git 'https://github.com/zaktales/gallery'
            }
        }
     }
}