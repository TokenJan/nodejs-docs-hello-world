pipeline {
    agent any
    stages {
        stage('build') {
            steps {
                echo 'build'
                sh 'docker build --tag helloworld:$(git log -1 --format=%h) .'
            }
        }
        stage('deploy:staging') {
            steps {
                echo 'deploy to staging env'
                sh 'docker stop helloworld-staging && docker rm helloworld-staging'
                sh 'docker run --name helloworld-staging -p 1338:1338 helloworld:$(git log -1 --format=%h) node /var/www/index.js &'
            }
        }
    }
}
