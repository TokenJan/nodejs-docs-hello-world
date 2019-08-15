pipeline {
    agent any
    stages {
        stage('build') {
            steps {
                echo 'build'
                sh 'docker build --tag helloworld:$BUILD_NUMBER .'
            }
        }
        stage('unit test') {
            steps {
                echo 'unit test'
            }
        }
        stage('dev') {
            steps {
                echo 'deploy to dev env'
                sh 'docker stop helloworld && docker rm helloworld'
                sh 'docker run --name helloworld -p 1337:1337 helloworld:$BUILD_NUMBER node /var/www/index.js &'
            }
        }
    }
}
