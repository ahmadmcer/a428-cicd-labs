node {
    stage('Initialization') {
        checkout scm
    }
    stage('Install Dependencies') {
        sh 'npm install'
    }
    stage('Testing') {
        sh 'CI=true npm test'
    }
}
