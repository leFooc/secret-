pipeline {
    agent any

    tools{
        maven 'maven'
        jdk 'jdk'
    }

    stages{
        stage('Build') {
            steps{
                sh 'mvn clean package'
                echo '>>> check structure'
                sh 'ls -lrt'
                echo '>>> check target'
                sh 'ls target -lrt'
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
                echo ">>> Deploy"
                deploy adapters: [tomcat9(credentialsId: 'tomcat', path: '', url: 'http://172.21.0.2:8080')], contextPath: '/app', war: '**/*.war'
//                   script {
//                         withCredentials([sshUserPrivateKey(credentialsId: 'tomcatSSH', keyFileVariable: 'mykey', passphraseVariable: '', usernameVariable: 'root')]) {
//                             // some block
//                             def remote=[name:'cba1ea6c7d02',host:'172.21.0.2',user:userName,identityFile:mykey,allowAnyHosts:true]
//
//                             sshCommand remote: remote, command: "ls -lrt"
//
//                             writeFile file:'abc.sh', text: 'ls -lrt'
//                             sshScript remote: remote, script: 'abc.sh'
//                             sshCommand remote: remote, command: "ls -lrt /usr/local/tomcat/webapps"
//                             //sshPut remote: remote, from 'target/*.war', into '/opt/tomcat/webapps/.'
//                         }
//                   }
                   //sh "scp -v -o StrictHostKeyChecking=no **/*.war root@172.21.0.2:/usr/local/tomcat/webapps/"
            }
        }
    }
}