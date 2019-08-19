pipeline {
    stage('checkout') {
        steps {
            git branch: "release-0.0.1", url: 'https://github.com/TokenJan/nodejs-docs-hello-world.git'
        }
    }
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
