pipeline {
    agent any
    tools {
        jdk 'JAVA_HOME'
        maven 'MAVEN_LATEST'
    }

    environment {
        JAVA_HOME = "${jdk}"
    }

    stages {
        stage('Prepare') {
            steps {
                checkout scm
            }
        }

        stage('Test') {
            steps {
                bat 'mvn install'
            }
        }

        stage('QA') {
            steps {
                withSonarQubeEnv('sonar') {
                    script {
                        def scannerHome = tool 'sonarqube-scanner'
                        bat "${scannerHome}/bin/sonar-scanner"
                    }
                }
            }
        }
    }
}
