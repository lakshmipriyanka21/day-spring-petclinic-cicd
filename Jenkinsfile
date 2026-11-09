
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
                withSonarQubeEnv('sonar-server') {
                    bat '''
                        mvn sonar:sonar ^
                        -Dsonar.projectKey=lakshmipriyanka21_day-spring-petclinic-cicd ^
                        -Dsonar.organization=lakshmipriyanka21 ^
                        -Dsonar.host.url=https://sonarcloud.io
                    '''
                }
            }
        }
    }
}
