node {
    try {
        stage('Checkout') {
            // Mengambil code dari repository
            checkout scm
        }

        // Mendefinisikan image docker
        docker.image('node:16-buster-slim').inside('-p 3000:3000') {
            
            stage('Build') {
                // Instalasi dependencies
                sh 'npm install'
            }

            stage('Test') {
                // Memberikan izin eksekusi agar tidak error "Permission denied"
                sh 'chmod +x ./jenkins/scripts/test.sh'
                
                // Menjalankan script test bawaan repository
                sh './jenkins/scripts/test.sh'
            }
        }
    } catch (e) {
        // Menangkap error jika pipeline gagal
        currentBuild.result = 'FAILURE'
        throw e
    }
}
