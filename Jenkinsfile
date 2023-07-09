pipeline {
    agent any
    stages {
        stage("Clone Git Repository") {
            steps {
                git(
                    url: "https://github.com/SagarKS18/ProjectPhase5.git",
                    branch: "master",
                    changelog: true,
                    poll: true
                )
            }
        }
        
        stage('Build and run application') {
            steps {
                sh 'java -jar jenkinsProject-0.0.1-SNAPSHOT.jar & echo $! > ./pid.file &'
          
                }
            }
        stage('Buffer Time') {
            steps {
                sleep(time: 1, unit: 'MINUTES')
            }
        }

        stage('Stop application') {
              steps {
                script {
                  sh 'kill -9 $(cat ./pid.file)'
                }
          }
        }
        
        stage("Push to Git Repository") {
            steps {
                withCredentials([gitUsernamePassword(credentialsId: '264a3ac1-b91e-4c28-b5eb-9cf3c687f567', gitToolName: 'Default')]) {
                    sh "git push -u origin master"
                }
            }
        }
    }
    post {
        always {
            deleteDir()
        }
    }
}
