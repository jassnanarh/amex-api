pipeline {
    agent { labels 'master'}
    tools {
        maven 'maven396' 
        jdk 'jdk17'
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
        cron('* /4 * * * *')
    }
    stages{
        stage('Checkout SCM') {
            steps {
                checkout SCM
                sh 'echo ${env.CHIEF_AUTHOR}'
            }
        }
        stage('Compile') {
            steps {
                sh 'maven compile'
            }
        }
    }

}
