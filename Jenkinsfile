pipeline {
    agent any

    tools {
        jdk 'JDK25'
        maven 'Maven'
    }

    environment {
        TOMCAT_WEBAPPS = 'C:\\apache-tomcat-9.0.117\\webapps'

    }

    stages {
        stage('Build') {
            steps {
                bat 'mvn clean package'
            }
        }

        stage('Test') {
            steps {
                bat 'mvn test'
            }
            post {
                always {
                    junit allowEmptyResults: true, testResults: 'target/surefire-reports/*.xml'
                }
            }
        }

        stage('Deploy') {
            steps {
                bat 'copy /Y target\\*.war "%TOMCAT_WEBAPPS%"'
            }
        }
    }

    post {
        success {
            echo 'Build, test, and deployment completed successfully.'
        }
        failure {
            echo 'Pipeline failed. Check console output.'
        }
    }
}