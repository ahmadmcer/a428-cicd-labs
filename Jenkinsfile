node {
    try {
        stage('Checkout') {
            checkout scm
        }

        docker.image('node:16-buster-slim').inside('-p 3000:3000') {
            
            stage('Build') {
                sh 'npm install'
            }

            stage('Test') {
                sh 'chmod +x ./jenkins/scripts/test.sh' 
                sh './jenkins/scripts/test.sh'
            }
            
            stage('Manual Approval') {
                input message: 'Lanjutkan ke tahap Deploy?', ok: 'Proceed'
            }

            stage('Deploy') {
                echo "Deploying application..."
                             
                sh '''
                    npm start &
                    PID=$!
                    echo "Aplikasi berjalan dengan PID: $PID. Menunggu 1 menit..."
                    sleep 60
                    echo "Waktu habis. Mematikan aplikasi..."
                    kill $PID || true
                '''
            }
        }
    } catch (e) {
        currentBuild.result = 'FAILURE'
        throw e
    }
}
