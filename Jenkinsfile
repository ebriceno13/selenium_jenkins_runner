pipeline {
    agent any
    stages {
        stage('Pull Latest Images') {
            steps {
                sh 'docker pull ebriceno13/testbuild'
                sh 'docker pull selenium/hub'
                sh 'docker pull selenium/node-chrome'
                sh 'docker pull selenium/node-firefox'
            }
        }
        stage('Start Grid') {
            steps {
                    sh "docker-compose up -d hub chrome firefox"
            }
        }
        stage('Run Test') {
            steps {
                     sh "docker-compose up firefoxrunnersearch firefoxrunneraccount chromerunner chromerunneraccount"
            }
        }
    }
    post{
        always{
            archiveArtifacts artifacts: 'output/**'
            sh 'docker-compose down'
            sh 'sudo rm -rf output/'
        }
    }
}