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
                    bat 'mvn clean verify sonar:sonar -Dsonar.projectKey=NAGP_devTestOPs -Dsonar.projectName="NAGP_devTestOPs" -Dsonar.host.url=http://localhost:9000 -Dsonar.token=sqp_1e03a2b51c5a9ac69fed019e5fb438e3e5033339'
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
