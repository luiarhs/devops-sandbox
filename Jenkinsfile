pipeline {
    agent any
    tools {
        maven 'MAVEN'
        jdk 'JDK11'
    }
    stages {
        // stage('checkout') {
        //     steps {
        //         git branch: 'main', credentialsId: 'github-luiarhs-up', url: 'https://github.com/luiarhs/devops-sandbox.git'
        //     }
        // }
        stage('Sonar scanner') {
            environment {
                BRANCH_NAME = "${env.BRANCH_NAME}"
                SCANNER_HOME = tool 'sonar-scanner'
                ACCESS_TOKEN = credentials('sonarcloud-poc-token')
            }
            steps {
                echo 'sonar scanner start...'
                withSonarQubeEnv('sonarcloud') {
                     sh '$SCANNER_HOME/bin/sonar-scanner -Dproject.settings=sonar.properties -Dsonar.projectKey=devops-sandbox-dev -Dsonar.login=$ACCESS_TOKEN -X'
                }
            }
            post {
                success {
                    echo 'Sonar stage executed successfully'
                }
                failure {
                    echo 'Sonar stage execution failed'
                }
            }
        }
        // stage("Quality Gate") {
        //     steps {
        //         timeout(time: 1, unit: 'HOURS') {
        //             waitForQualityGate abortPipeline: true
        //         }
        //     }
        // }
    }
    post {
        // always{
        //     echo 'always'
        // }
        success{
            echo 'pipeline executed successfully'
        }
        failure{
            echo 'pipeline execution failed'
        }
    }
}