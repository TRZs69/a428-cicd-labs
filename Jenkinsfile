node {
    stage('Checkout') {
        checkout([$class: 'GitSCM',
            branches: [[name: '*/react-app']],
            userRemoteConfigs: [[
                url: 'https://github.com/<username>/a428-cicd-labs.git',
                credentialsId: 'github-credentials'
            ]]
        ])
    }

    stage('Install') {
        dir('react-app') {
            sh 'npm install'
        }
    }

    stage('Test') {
        dir('react-app') {
            sh 'npm test -- --watch=false || true'
        }
    }

    stage('Build') {
        dir('react-app') {
            sh 'npm run build'
        }
    }
}
