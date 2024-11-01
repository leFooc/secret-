pipeline {
    agent any

    tools{
        maven: 'mAvEn'
    }

    stages{
        stage('Build') {
            steps{
                sh 'mvn clean package'
            }
            post{
                success{
                    archiveArtifacts artifacts: '**/target/*.war'
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
                deploy adapters: [tomcat9(credentialsId: 'tomcat', path: '', url: 'http:172.17.0.2')], contextPath: null, war: '*/.war'
            }
        }
    }
}