node {
    stage('Checkout') {
        checkout scm
    }

    stage('Install') {
        dir('react-app') {
            sh 'npm install'
            // kalau ada package-lock.json, lebih bagus:
            // sh 'npm ci'
        }
    }

    stage('Build') {
        dir('react-app') {
	    sh 'npm run build'
    	}
    }

    stage('Test') {
        dir('react-app') {
            sh 'CI=true npm test -- --watchAll=false'
        }
    }

    stage('Manual Approval') {
        timeout(time: 5, unit: 'MINUTES') {
            input message: 'Lanjutkan ke tahap Deploy?'
        }
    }

    stage('Deploy') {
        dir('react-app') {
            // Jalankan app di background, simpan PID biar matinya presisi
            sh '''
              nohup npm start > app.log 2>&1 &
              echo $! > app.pid
            '''

            echo 'Aplikasi berjalan selama 1 menit...'
            sleep 60

            // Matikan hanya proses yang kamu start
            sh '''
              if [ -f app.pid ]; then
                kill $(cat app.pid) || true
                rm -f app.pid
              fi
            '''
        }
    }
}
