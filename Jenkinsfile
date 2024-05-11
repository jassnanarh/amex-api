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
    triggers {
        pollSCM('*/5 * * * *')
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
    }

}
             
