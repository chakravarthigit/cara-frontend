pipeline {
  agent any

  tools {
    nodejs 'Node 18'  // 👈 Must match exactly what is in Jenkins global config
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
          yarn -v || npm install -g yarn
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
