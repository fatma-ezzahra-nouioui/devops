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
       stage('MOCKITO') {
    steps {
        sh 'mvn clean test jacoco:report'
    }
    post {
        always {
            junit '**/target/surefire-reports/TEST-*.xml'
            publishHTML(target: [
                allowMissing: false,
                alwaysLinkToLastBuild: true,
                keepAll: true,
                reportDir: 'target/site/jacoco',
                reportFiles: 'index.html',
                reportName: 'JaCoCo Code Coverage'
            ])
        }
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
