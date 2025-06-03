pipeline {
  agent any

  stages {
    stage('Install Node 18') {
      steps {
        // Download and install Node.js 18
        sh '''
          curl -fsSL https://nodejs.org/dist/v18.0.0/node-v18.0.0-linux-x64.tar.xz -o node-v18.tar.xz
          tar -xf node-v18.tar.xz
          export PATH=$PWD/node-v18.0.0-linux-x64/bin:$PATH
          node -v
          npm -v
        '''
      }
    }
    stage('Checkout') {
      steps {
        git 'https://github.com/chakravarthigit/cara-frontend.git'
      }
    }
    stage('Install Dependencies') {
      steps {
        sh '''
          export PATH=$PWD/node-v18.0.0-linux-x64/bin:$PATH
          npm install
        '''
      }
    }
    stage('Build Android') {
      steps {
        dir('android') {
          sh './gradlew assembleRelease'
        }
      }
    }
    stage('Archive APK') {
      steps {
        archiveArtifacts artifacts: '**/*.apk', fingerprint: true
      }
    }
  }
}
