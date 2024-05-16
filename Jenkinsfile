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
        stage("Docker Build & Push"){
            steps{
                script{
                   withDockerRegistry(credentialsId: 'fe107e6f-4a87-4d7e-92af-b8a89cf17c29', toolName: 'docker') {
                        
                        sh "docker build -t image1 ."
                        sh "docker tag image1 akhil146/spring123:latest "
                        sh "docker push akhil146/spring123:latest "
                    }
                }
            }
        }

    }
}

