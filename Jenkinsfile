pipeline {
    agent any
    
    tools {
        jdk 'jdk11'
        maven 'maven3'
    }
    environment {
        SCANNER_HOME= tool 'sonar-scanner'
    }
   
       stages {
        stage('Git Checkout ') {
            steps {
                git branch: 'main', changelog: false, poll: false, url: 'https://github.com/akhilesh-007/SpringBoot-WebApplication.git'
            }
        }   
        stage('Code Compile') {
            steps {
                    sh "mvn compile"
            }
        }
        
        stage('Run Test Cases') {
            steps {
                    sh "mvn test"
            }
        }
        stage('Sonar Analysis') {
            steps {
               withSonarQubeEnv('sonar-server'){
                   sh ''' $SCANNER_HOME/bin/sonar-scanner -Dsonar.projectName=Springboot \
                   -Dsonar.java.binaries=. \
                   -Dsonar.projectKey=Springboot '''
               }
            }
        }
      // jar file /var/lib/jenkins/workspace/Springboot
      
      stage('Package') {
            steps {
                    sh "mvn package"
            }
        }

    }
}

