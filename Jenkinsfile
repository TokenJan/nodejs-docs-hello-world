pipeline {
    agent any
    stages {
        stage('pre-build') {
            parallel {
                stage('style check') {
                    steps {
                        echo 'style check'
                    }
                }
                stage('find bugs') {
                    steps {
                        echo 'find bugs'
                    }
                }
                stage('unit test') {
                    steps {
                        echo 'unit test'
                    }
                }
            }
        }
        stage('build') {
            steps {
                echo 'build'
                sh 'docker build --tag helloworld:$(git log -1 --format=%h) .'
                sh 'docker stop helloworld-staging && docker rm helloworld-staging'
                sh 'docker run --name helloworld-staging -p 1338:1338 helloworld:$(git log -1 --format=%h) node /var/www/index.js &'
            }
        }
    }
}
