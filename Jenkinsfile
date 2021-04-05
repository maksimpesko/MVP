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
        stage ('Deploy') {
            agent {node {label 'jenkins-artifactory'}}
            steps {
                dir('/home/jenkins'){
                unstash 'build_app'
                sh 'ls -la'
                }
            }
        }
    }

}
