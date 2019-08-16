node {
    stage('build') {
        echo 'build'
        sh 'docker build --tag helloworld:$(git log -1 --format=%h) .'
    }
    stage('deploy:qa') {
        echo 'deploy to qa env'
        sh 'docker run --name helloworld-qa -p 1338:1338 helloworld:$(git log -1 --format=%h) node /var/www/index.js &'
    }
    stage('smoke test') {
        echo 'smoke test'
    }
    stage('full regression test') {
        echo 'full regression test'
    }
}
