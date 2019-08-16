node {
    stage('deploy:qa') {
        steps {
            echo 'deploy to qa env'
            sh 'docker stop helloworld && docker rm helloworld'
            sh 'docker run --name helloworld -p 1338:1338 helloworld:$(git log -1 --format=%h) node /var/www/index.js &'
        }
    }
}
