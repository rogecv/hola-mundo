pipeline {
    agent any
    
    stages {
        stage('Checkout') {
            steps {
                slackNotif.initStageMessage()
                git 'https://github.com/rogecv/hola-mundo.git'
                slackNotif.updateStageMessage()
            }
        }
        
        stage('Build') {
            steps {
                slackNotif.initStageMessage()
                sh 'mvn clean install'
                slackNotif.updateStageMessage()
            }
        }

        stage('Scan Code'){
            steps{
                slackNotif.initStageMessage()
                script{
                    sh 'mvn sonar:sonar'
                }
                slackNotif.updateStageMessage()
            }
        }
        
        stage('Test') {
            steps {
                slackNotif.initStageMessage()
                sh 'mvn test'
                slackNotif.updateStageMessage()
            }
        }

        stage('Deploy'){
            steps{
                slackNotif.initStageMessage()
                sh ''
                slackNotif.updateStageMessage()
            }
        }
    }
}
