node {
     properties([
         parameters([
             gitParameter(branch: '',
                          branchFilter: 'origin/(.*)',
                          defaultValue: 'release-0.0.1',
                          description: '',
                          name: 'BRANCH',
                          quickFilterEnabled: false,
                          selectedValue: 'NONE',
                          sortMode: 'NONE',
                          tagFilter: '*',
                          type: 'PT_BRANCH')
         ])
     ])
    stage('build') {
        echo 'build'
        sh 'docker build --tag helloworld:$(git log -1 --format=%h) .'
    }
    stage('deploy:staging') {
        echo 'deploy to staging env'
        sh 'docker stop helloworld-staging && docker rm helloworld-staging'
        sh 'docker run --name helloworld-staging -p 1338:1338 helloworld:$(git log -1 --format=%h) node /var/www/index.js &'
    }
    stage('smoke test') {
        echo 'smoke test'
    }
    stage('full regression test') {
        echo 'full regression test'
    }
}
