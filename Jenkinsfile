pipeline {
    agent any
    environment {
        PATH = "$PATH:C:/apache-maven-3.8.6/bin"
    }
    stages{
        stage("Get Code"){
            steps{
                git branch: 'master', changelog: false, poll: false, url: 'https://github.com/PraverChaurasia/devTest_NAGP_2023_final.git/'
            }
        }
        stage('Build Code'){
            steps{
                bat 'mvn clean test'
            }
        }
        stage('Sonar Qube'){
            steps{
                withSonarQubeEnv('sonar_qube'){
                    bat 'mvn clean verify sonar:sonar'
                }
            }
        }
    }    

    post {
        success {
            echo 'Pipeline succeeded!'
        }
        
        failure {
            echo 'Pipeline failed!'
        }
    }
}
