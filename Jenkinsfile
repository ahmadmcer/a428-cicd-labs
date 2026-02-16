node {
    def dockerImage

    stage('Checkout') {
        // Mengambil code dari repository
        checkout scm
    }

    stage('Build Docker Image') {
        // Membangun image docker untuk environment testing
        dockerImage = docker.build("node-app:test", ".") 
    }

    stage('Test') {
        // Menjalankan test di dalam container
        dockerImage.inside {
            sh 'npm install'
            sh 'npm test' 
        }
    }
}
