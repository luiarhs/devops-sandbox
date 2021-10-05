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
        stage('Sonar analysis by webhook') {
            environment {
                scannerHome = tool 'sonar-scanner'
            }
            steps {
                echo 'sonar scanner start...'
                // withSonarQubeEnv('sonarcloud') {
                //     sh "${scannerHome}/bin/sonar-scanner -Dproject.settings=sonar-project.properties -X "
                // }
                withSonarQubeEnv ('sonarcloud') {
                    sh "${scannerHome}/bin/sonar-scanner -Dsonar.organization=luiarhs -Dsonar.host.url=https://sonarcloud.io -Dsonar.projectKey=luiarhs_devops-sandbox -Dsonar.login=4df569cfc2ffb87004c5d721650c4854ddad4ae3 -Dsonar.projectName=sonnarcloud-poc -Dsonar.projectName=PoC -Dsonar.projectVersion=1.0 -Dsonar.language=java -Dsonar.sources=src/main/java -Dsonar.java.binaries=target/classes -Dsonar.sourceEncoding=UTF-8 -X"
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