pipeline {
    agent { label 'master'}
    tools {
        maven 'maven' 
        jdk 'jdk11'
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
                checkout SCM
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
