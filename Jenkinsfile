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
        
        stage('Java/Docker Version') {
            sh "java -version"
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

        stage('Package Build') {
            dir('xp') {
                sh "tar -zcvf build.tar.gz build/"
            }
        }

        stage('Artifacts Creation') {
            dir('xp') {
                fingerprint 'build.tar.gz'
                archiveArtifacts 'build.tar.gz'
                echo "Artifact stored"
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