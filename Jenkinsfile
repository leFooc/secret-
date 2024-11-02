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
                  //deploy adapters: [tomcat9(credentialsId: '1', path: '', url: 'http://172.21.0.2:8080/')], contextPath: null, war: '**/*.war'
                  script {
                        withCredentials([sshUserPrivateKey(credentialsId: 'tomcatSSH', keyFileVariable: 'mykey', assphraseVariable: '', usernameVariable: 'userName')]) {
                            // some block
                            def remote=[name:'test',host:'172.21.0.2',user:userName,identityFile:mykey,allowAnyHosts:true]

                            sshCommand remote: remote, command: "ls -lrt"

                            writeFile file:'abc.sh', text: 'ls -lrt'
                            sshScript remote: remote, script: 'abc.sh'
                            sshCommand remote: remote, command: "ls -lrt /usr/local/tomcat/webapps"
                            //sshPut remote: remote, from 'target/*.war', into '/opt/tomcat/webapps/.'
                        }
                  }
            }
        }
    }
}