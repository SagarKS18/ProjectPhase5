pipeline {
    agent any
    stages {
        stage("Clone Git Repository") {
            steps {
                git(
                    url: "https://github.com/Vin200/projectPhase5.git",
                    branch: "master",
                    changelog: true,
                    poll: true
                )
            }
        }
        
        stage('Build and run application') {
            steps {
                sh 'java -jar projectPhase5-0.0.1-SNAPSHOT.jar & echo $! > ./pid.file &'
          
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
                withCredentials([gitUsernamePassword(credentialsId: '96fd7231-9ac1-49b5-9856-396ff544a983', gitToolName: 'Default')]) {
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