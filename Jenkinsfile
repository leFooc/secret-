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
              script{
                withCredentials([sshUserPrivateKey(credentialsId: 'tomcatKey',keyFileVariable:'myKey',usernameVariable:'root')]){
                  def remote = [name:'lcfc21b43f19',host:'172.21.0.2',user:root,identityFile:myKey,allowAnyHosts:true]
                  sshPut remote: remote, from: '**/*.war', into '/usr/local/tomcat/webapps/.'
                }
              }
            }
        }
    }
}