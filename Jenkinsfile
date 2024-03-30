pipeline {
    agent any
    
    stages {
        stage('Checkout') {
            steps {
                git 'https://github.com/rogecv/hola-mundo.git'
            }
        }
        
        stage('Build') {
            steps {
                sh 'mvn clean install'
            }
            post{
                    Success{
                        slackSend channel1: '#notificacionPipeline',
                                    message: "Build OK"
                    }
                    Failed{
                        slackSend channel1: '#notificacionPipeline',
                                    message: "Build Fail"
                    }
                }
            }
        }

        stage('Scan Code'){
            steps{
                script{
                    sh 'mvn sonar:sonar'
                }
                post{
                    Success{
                        slackSend channel1: '#notificacionPipeline',
                                    message: "Scan OK"
                    }
                    Failed{
                        slackSend channel1: '#notificacionPipeline',
                                    message: "Scan Fail"
                    }
                }
            }
        }
        
        stage('Test') {
            steps {
                sh 'mvn test'
            }
            post{
                    Success{
                        slackSend channel1: '#notificacionPipeline',
                                    message: "Build OK"
                    }
                    Failed{
                        slackSend channel1: '#notificacionPipeline',
                                    message: "Build Fail"
                    }
                }
        }

        stage('Deploy to test'){
             when {
                expression { currentBuild.result == 'SUCCESS' } }
            steps{
                sh 'ansible-playbook deploy_to_test.yml'
            }
            post{
                    Success{
                        slackSend channel1: '#notificacionPipeline',
                                    message: "Test OK"
                    }
                    Failed{
                        slackSend channel1: '#notificacionPipeline',
                                    message: "Test Fail"
                    }
                }
        }
    }
}
