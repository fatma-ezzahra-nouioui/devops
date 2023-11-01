pipeline {
    agent any
    stages {
        stage('Build') {
            steps {
                sh 'mvn clean'
            }
            
        } 
        stage('Compile') {
            steps {
                sh 'mvn compile'  
            }
        }
        stage ('Code Quality'){
            steps {
                    withSonarQubeEnv('SonarQubeServer') {
                sh 'mvn sonar:sonar'
                }
             }
        }
    
    }
}
