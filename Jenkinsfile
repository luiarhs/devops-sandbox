pipeline {
    agent any
    tools {
        maven 'MAVEN'
        jdk 'JDK11'
    }
    stages {
        stage('checkout') {
            steps {
                git branch: 'main', credentialsId: 'github-luiarhs-up', url: 'https://github.com/luiarhs/devops-sandbox.git'
            }
        }
        stage('Sonar analysis by webhook') {
            environment {
                scannerHome = tool 'sonar-scanner'
            }
            steps {
                echo 'sonar scanner start...'
                withSonarQubeEnv('sonarcloud') {
                    sh "${scannerHome}/bin/sonar-scanner -X -Dsonar.projectKey=luiarhs_devops-sandbox -Dsonar.sources=."
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
        // stage('Sonar analysis by token') {
        //     when {
        //         branch 'main'
        //     }
        //     environment {
        //         scannerHome = tool 'sonar-scanner'
        //     }
        //     steps {
        //         withSonarQubeEnv(installationName: 'sonarcloud-server', credentialsId: 'sonarcloud-secret', envOnly: true) {
        //             // 083c7c9dd594fc14da7a28d6a93d7719fc6e42b4
        //             // This expands the evironment variables SONAR_CONFIG_NAME, SONAR_HOST_URL, SONAR_AUTH_TOKEN that can be used by any script.
        //             sh "${scannerHome}/bin/sonar-scanner -X"
        //         }
        //     }
        //     post {
        //         success {
        //             echo 'Sonar stage executed successfully'
        //         }
        //         failure {
        //             echo 'Sonar stage execution failed'
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