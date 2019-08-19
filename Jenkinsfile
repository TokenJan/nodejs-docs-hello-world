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
    stage('style check') {
        echo 'style check'
    }
     stage('find bugs') {
        echo 'find bugs'
    }
    stage('unit test') {
        echo 'unit test'
    }
    stage('build') {
        echo 'build'
        sh 'docker build --tag helloworld:$(git log -1 --format=%h) .'
    }
    stage('publish') {
        echo 'push to docker registry'
    }
    stage('deploy:dev') {
        parallel 'deploy': {
            stage('deploy') {
                echo 'deploy to dev env'
                sh 'docker stop helloworld && docker rm helloworld'
                sh 'docker run --name helloworld -p 1337:1337 helloworld:$(git log -1 --format=%h) node /var/www/index.js &'
            }
        }, 'Contract Test': {
                stage('contract test') {
                       echo 'contract test'
                }
        }, 'SonarQube': {
                stage('sonarqube scanning') {
                       echo 'sonarqube scanning'
                }
        }     
    }
}
