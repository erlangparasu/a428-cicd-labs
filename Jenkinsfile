    pipeline {
        agent {
            docker {
                image 'node:16-buster-slim' 
                args '-p 3000:3000' 
            }
        }
        stages {
            stage('Build') { 
                steps {
                    echo 'info: build'
                    sh 'npm install'
                }
            }
            stage('Test') {
                steps {
                    echo 'info: test'
                    sh './jenkins/scripts/test.sh'
                }
            }
            stage('Manual Approval') {
                steps {
                    echo 'info: approval'
                    sh './jenkins/scripts/kill.sh'
                    input message: 'Lanjutkan ke tahap Deploy? (Klik "Proceed" untuk deploy)'
                }
            }
            stage('Deploy') {
                steps {
                    echo 'info: deploy'
                    sh './jenkins/scripts/deliver.sh'
                    sleep 60
                    sh './jenkins/scripts/kill.sh'
                }
            }
        }
    }
