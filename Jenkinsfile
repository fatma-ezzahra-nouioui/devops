pipeline {
    agent any
    stages {
        stage('Build') {
            steps {
                script {
                    sh 'mvn clean'
                }
            }
        }
        stage('Compile') {
            steps {
                script {
                    sh 'mvn compile'
                }
            }
        }
        stage('JaCoCo Code Coverage') {
            steps {
                script {
                    sh 'mvn clean test org.jacoco:jacoco-maven-plugin:prepare-agent'
                }
            }
        }
        stage('Code Quality') {
            steps {
                script {
                    withSonarQubeEnv('SonarQubeServer') {
                        sh 'mvn sonar:sonar'
                    }
                }
            }
        }
        stage('MOCKITO') {
            steps {
                script {
                    sh 'mvn test'
                }
            }
            post {
                always {
                    junit '**/target/surefire-reports/TEST-*.xml'
                }
            }
        }
        stage('Artifact construction') {
            steps {
                script {
                    sh 'mvn package'
                }
            }
            post {
                success {
                    archiveArtifacts artifacts: 'target/*.jar', allowEmptyArchive: true
                }
            }
        }
    }
}