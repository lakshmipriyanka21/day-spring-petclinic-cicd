


pipeline {
    agent any

    tools {
        maven 'Maven'
    }

    stages {
        stage('Checkout') {
            steps {
                checkout scm
            }
        }

        stage('Validate') {
            steps {
                bat 'mvn validate'
            }
        }

        stage('Compile') {
            steps {
                bat 'mvn compile'
            }
        }

        stage('Test') {
            steps {
                bat 'mvn test'
            }
        }

        stage('Package') {
            steps {
                bat 'mvn package'
            }
        }

        stage('SonarQube Analysis') {
            steps {
                script {
                    def scannerHome = tool 'sonar-scanner'

                    withSonarQubeEnv('sonar-server') {
                        withEnv(["SCANNER_HOME=${scannerHome}"]) {
                            bat '''
                            @echo off
                            call "%SCANNER_HOME%\\bin\\sonar-scanner.bat" ^
                            -Dsonar.projectKey=lakshmipriyanka21_day-spring-petclinic-cicd ^
                            -Dsonar.organization=lakshmipriyanka21 ^
                            -Dsonar.host.url=https://sonarcloud.io ^
                            -Dsonar.sources=src/main ^
                            -Dsonar.java.binaries=target/classes
                            '''
                        }
                    }
                }
            }
        }

        stage('Docker Build') {
            steps {
                bat 'docker build -t day40-petclinic:latest .'
            }
        }
    }
}
