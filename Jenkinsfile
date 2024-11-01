pipeline {
    agent any

    tools{
        maven 'mAvEn'
        jdk 'jdk'
    }

    stages{
        stage('Build') {
            steps{
                sh 'mvn clean package'
            }
            post{
                success{
                    archiveArtifacts artifacts: '**/target/*.war'
                    sh 'ls -l'
                }
            }
        }
        stage('Test') {
            steps{
                echo '>>> Test'
            }
        }
        stage('Deploy') {
            steps{
              deploy adapters: [tomcat9(credentialsId: '1', path: '', url: 'http://172.21.0.2')], contextPath: 'usr/local/tomcat/webapps/app', war: '*/.war'
            }
        }
    }
}