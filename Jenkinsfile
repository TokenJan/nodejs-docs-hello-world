node {
    stage('deploy:qa') {
        echo 'deploy to qa env'
        sh 'docker run --name helloworld-qa -p 1338:1338 helloworld:$(git log -1 --format=%h) node /var/www/index.js &'
    }
}
