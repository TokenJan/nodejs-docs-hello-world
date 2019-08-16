properties([
           parameters([
                   string(name: 'URL', defaultValue: 'https://github.com/TokenJan/nodejs-docs-hello-world.git'),
                   string(name: 'BRANCH', defaultValue: 'master'),
           ])
])

node {
    stage('checkout') {
        checkout ( [$class: 'GitSCM',
        branches: [[name: '${BRANCH}' ]],
        userRemoteConfigs: [[
        credentialsId: '5c73d461-8fee-4434-9f63-26e45e845e69', 
        url: '${URL}']]])    
    }
    stage('build') {
        echo 'build'
        sh 'docker build --tag helloworld:$(git log -1 --format=%h) .'
    }
    stage('unit test') {
        echo 'unit test'
    }
    stage('deploy:dev') {
        echo 'deploy to dev env'
        sh 'docker stop helloworld && docker rm helloworld'
        sh 'docker run --name helloworld -p 1337:1337 helloworld:$(git log -1 --format=%h) node /var/www/index.js &'
    }
}
