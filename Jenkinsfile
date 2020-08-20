node {
    try {        
        stage('Checkout Github') {
            checkout scm
        }
        
        stage('Node/Npm Version') {
            nodejs('nodejs') {
                sh "node --version"
                sh "npm --version"
            }
        }
        
        stage('Java Version') {
            sh "java -version"
        }
        
        stage('Java Version') {
            sh "docker -v"
        }
        
        stage('Install Dependencies') {
            dir('xp') {
                sh "yarn install"
            }
        }
        
        stage('Build Project') {
            dir('xp') {
                sh "yarn build"
            }
        }

        stage('Build new docker image') {
            sh 'docker image build -t xp/xp-react:latest .'
        }
        
        stage('Stop and remove old container') {
            // sh 'docker stop shield_ui && docker rm shield_ui'
        }

        stage('Run Container') {
            sh 'docker run -d --name xp-react -p 8081:80 xp/xp-react:latest'
        }
        
    } catch(e) {
        throw e
    } finally {
        echo 'JOB FINISHED'
    }
}