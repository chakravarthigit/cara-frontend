pipeline {
  agent any

  stage('Checkout') {
  steps {
    git branch: 'main', url: 'https://github.com/chakravarthigit/cara-frontend.git'
  }
}

    stage('Install Dependencies') {
      steps {
        sh 'yarn install'
      }
    }
    // Test stage removed as requested
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
