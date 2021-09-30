pipeline {
    agent any
    tools {
        maven 'MAVEN'
        jdk 'JDK11'
    }
    stages {
        stage('Git Checkout') {
            steps {
                git branch: 'main', credentialsId: 'dp-github-integrator', url: 'https://github.com/ab-inbev-global-martech/devops-sandbox.git'
            }
            post {
                success {
                    echo 'git checkout executed successfully'
                }
                failure {
                    echo 'git checkout execution failed'
                }
            }
        }
        stage('Sonar analysis by webhook') {
            when {
                branch 'main'
            }
            environment {
                scannerHome = tool 'sonar-scanner'
            }
            steps {
                withSonarQubeEnv('sonarcloud') {
                    sh "${scannerHome}/bin/sonar-scanner -X"
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
        //     whe
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