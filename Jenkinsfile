node {

    stage('Checkout') {
        checkout scm
    }

    stage('Install') {
        dir('react-app') {
            sh 'npm install'
        }
    }

    stage('Test') {
        dir('react-app') {
            sh 'npm test -- --watch=false'
        }
    }

    stage('Manual Approval') {
        timeout(time: 5, unit: 'MINUTES') {
            input message: 'Lanjutkan ke tahap Deploy?'
        }
    }

    stage('Deploy') {
        dir('react-app') {
            // Start app di background
            sh 'npm start &'

            echo 'Aplikasi berjalan selama 1 menit...'
            sleep 60

            // Matikan setelah 1 menit
            sh 'pkill node || true'
        }
    }
}


