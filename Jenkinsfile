pipeline {
  agent any

  environment {
    // Optional: adjust PATH if node/yarn are in custom directories
    PATH = "/usr/local/bin:/usr/bin:$PATH"
  }

  stages {
    stage('Checkout') {
      steps {
        git branch: 'main', url: 'https://github.com/chakravarthigit/cara-frontend.git'
      }
    }

    stage('Install Dependencies') {
      steps {
        sh '''
          node -v || curl -fsSL https://deb.nodesource.com/setup_18.x | sudo -E bash -
          node -v || sudo apt-get install -y nodejs
          yarn -v || sudo npm install -g yarn
          yarn install
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
        archiveArtifacts artifacts: 'android/app/build/outputs/**/*.apk', fingerprint: true
      }
    }
  }
}
