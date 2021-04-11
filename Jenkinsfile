pipeline {
    agent {node {label 'jenkins-slave'}}

    stages {
        stage ('Checkout project repository') {
            steps {
                git branch: 'main', url: 'https://github.com/artsiompeshko/java-build-tools.git'
            }
        }
        stage ('Execute unit tests') {
            when {
                expression {
                    currentBuild.result == null || currentBuild.result == 'SUCCESS'
                }
            }
            steps {
                sh 'chmod +x gradlew'
                sh './gradlew test'
            }
        }
        stage ('Prepare build artifact') {
            steps {
                sh './gradlew build'
                stash includes: '**', name: 'build_app'
            }
        }
        stage ('Build') {
            agent {node {label 'jenkins-artifactory'}}
            steps {
                dir('/home/jenkins'){
                unstash 'build_app'
                sh './gradlew appRun'
<<<<<<< HEAD
                sh 'curl localhost:8080/web'
=======
>>>>>>> 89110eac9b2129f915ea6e282a73f260e3865e1f
                }
            }
        }
    }
}
