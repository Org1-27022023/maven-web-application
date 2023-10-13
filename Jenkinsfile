pipeline {
    agent any
    
    tools {
        maven "maven 3.9.4"
    }

    options {
        buildDiscarder logRotator(artifactDaysToKeepStr: '', artifactNumToKeepStr: '', daysToKeepStr: '3', numToKeepStr: '3')
        timestamps()
    }
    
    

    stages {
        stage('Checkout code') {
            steps {
                git branch: 'development', credentialsId: 'git cred', url: 'https://github.com/Organi2/maven-web-application.git'
            }
        }

        stage('build package') {
            steps {
                bat "mvn clean package"
            }
        }

        stage('sonar report') {
            steps {
                bat "mvn sonar:sonar"
            }
        }

        stage('upload artifacts') {
            steps {
                bat "mvn deploy"
            }
        }

        stage('deploy to tomcat') {
            steps {
                bat "copy C:\\ProgramData\\Jenkins\\.jenkins\\workspace\\declarative\\target\\maven-web-application.war C:\\Users\\ADMIN\\Downloads\\apache-tomcat-9.0.73\\apache-tomcat-9.0.73\\webapps"
            }
        }
    }
}
