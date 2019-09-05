properties([
           parameters([
                   string(name: 'URL', defaultValue: 'https://github.com/TokenJan/nodejs-docs-hello-world.git'),
                   string(name: 'BRANCH', defaultValue: 'master'),
           ])
])

pipeline {
    agent any
    environment {
        GITVERSION   = 'gittools/gitversion:5.0.0-linux-debian-9-netcoreapp2.2'
    }
    stages {
        stage('checkout') {
            steps {
                checkout ( [$class: 'GitSCM',
                branches: [[name: '${BRANCH}' ]],
                userRemoteConfigs: [[
                credentialsId: '5c73d461-8fee-4434-9f63-26e45e845e69', 
                url: '${URL}']]]) 
                script {
                      SEMVER = sh(returnStdout: true, script: 'docker run --rm --volume "$(pwd):/repo" $GITVERSION /repo -output json -showvariable FullSemVer')
                }
            }
        }
        stage('pre-build') {
            parallel {
                stage('style check') {
                    steps {
                        echo 'style check'
                    }
                }
                stage('TSLint') {
                    steps {
                        echo 'TSLint'
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
                sh 'docker build --tag helloworld:$(docker run --rm --volume "$(pwd):/repo" $GITVERSION /repo -output json -showvariable FullSemVer) .'
            }
        }
        stage('publish') {
            steps {
                echo 'push to docker registry'
            }
        }
        stage('deploy:dev') {
            parallel {
                stage('deploy') {
                    steps {
                        echo 'deploy to dev env'
                        sh 'docker stop helloworld && docker rm helloworld'
                        sh 'docker run --name helloworld -p 1337:1337 helloworld:$(docker run --rm --volume "$(pwd):/repo" $GITVERSION /repo -output json -showvariable FullSemVer) node /var/www/index.js &'
                    }
                }
                stage('contract test') {
                    steps {
                        echo 'contract test'
                    }
                }
                stage('sonarqube scanning') {
                    steps {
                        echo 'sonarqube scanning'
                    }
                }
            }   
        }
    }
}
