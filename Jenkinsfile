pipeline {
    agent { label 'JDK-8'}
    parameters {
        choice(name: 'BUILD', choices: ['dev-1', 'master'], description: 'Branch to build')
        string(name: 'MAIN-GOAL', defaultValue: 'clean package', description: 'maven goal')
    }
    triggers {
        pollSCM('* * * * *')
    }
    stages {
        stage ('source code  from git remote repository') {
            steps {
                git url: "https://github.com/ksumankumar/game-of-life.git",
                 branch: "${params.BUILD}"
            }
        }
        stage('To build maven package') {
            steps {
                sh "mvn ${params.MAIN-GOAL}"
            }
        }
        stage("archive artifact") {
            steps {
                archiveArtifacts artifacts: '**/*.jar'
            }
        }
        stage("junit Reports") {
            steps {
                junit '**/surefire-reports/*.xml'
            }
        }
    }
}

