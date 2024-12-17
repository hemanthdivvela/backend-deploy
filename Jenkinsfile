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
    parameters {
        string(name: 'appVersion', defaultValue: '1.1.0', description: 'what is the application version?')
    }
    environment{
        def appVersion = '' //variable declartion in gobal
        nexusUrl = '44.192.3.23:8081'
    }
       
    stages {
        stage('print  the version'){
            steps {
                script{

                    echo "application version: ${params.appVersion}"
                }
            }
        }
        stage('Init'){
            steps {
                sh """
                    cd terraform
                    terraform init

                """  
            }
        }
        stage('Plan'){
            steps {
                sh """
                    cd terraform
                    terraform plan -var="app_version=${params.appVersion}"

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
            echo 'I will run when pipline is success!'
        }
        failure { 
            echo 'I will run when pipline is failure!'
        }
    }
}  