pipeline {
    agent {
        label 'AGENT-1'
    }
    options {
        // Timeout counter starts AFTER agent is allocated
        timeout(time: 30, unit: 'MINUTES')
        disableConcurrentBuilds()
        ansiColor('xterm')
    }
    stages {
        stage('read the version'){
            steps{
                script{
                    def packageJson = readJSON file: 'package.json'
                    def appVersion = packageJson.version
                    echo "application version: $appVersion"
                }
            }
        }
        stage('Install Dependencies') {
            steps {
                sh """
                npm install
                ls -ltr
                echo "application version: $appVersion"
                """
            }
        }
    }    
    post { 
        always { 
            echo 'I will always say Hello again!'
            deleteDir()
        }
        success {
            echo 'I will run when pipeline is success'
        }
          failure {
            echo 'I will run when pipeline is failed'
        }
    }
}