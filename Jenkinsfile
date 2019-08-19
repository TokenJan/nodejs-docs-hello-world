pipeline {
    agent any
    stages {
        stage('build') {
            steps {
                echo 'build'
                sh 'docker build --tag helloworld:$(git log -1 --format=%h) .'
            }
        }
    }
}
