pipeline {
    agent { label 'master'}
    tools { 
        jdk 'jdk17'
        maven 'maven'
    }
    environment {
        CHIEF_AUTHOR = 'ASHER'
        RETRY_COUNT = 3
    }
    options { 
        buildDiscarder(logRotator(numToKeepStr: '3')) 
        disableConcurrentBuilds()
        quietPeriod(5)
    }
    parameters {
        choice(name: 'TARGET_ENV', choices: ['UAT', 'SIT', 'STAGING'], description: 'Pick something')
    }
    stages{
        stage('Checkout SCM') {
            steps {
                checkout scm
                sh "echo $CHIEF_AUTHOR"
            }
        }
        stage('Compile') {
            steps {
                sh 'mvn compile'
            }
        }
       stage('Code Scan') {
            steps {
                withSonarQubeEnv('pragra-sonar') {
                    sh 'mvn  -Dsonar.projectKey=jassnanarh_amex-api -Dsonar.organization=jassnanarh org.sonarsource.scanner.maven:sonar-maven-plugin:3.7.0.1746:sonar'
                }
               
            }
        }
        stage('Test') {
            steps {
                sh 'mvn test'
            }
        }
        stage('Package') {
            steps {
                sh 'mvn package'
                sh 'echo done'
            }
        }
    }
    post {
        always {
            emailext attachLog: true, body: 'hello', subject: "BUILD STATUS $JOB_NAME", to: 'kaurjass261997@gmail.com, prabhjotsingh326@gmail.com'
        }
        success {
            mail bcc: '', body: 'HELLO', cc: '', from: '', replyTo: '', subject: 'BUILD SUCCESS FULL $JOB_NAME', to: 'kaurjass261997@gmail.com , prabhjotsingh326@gmail.com'
        }
            
    }
}

    

            
            


             
