pipeline {
  agent any

  stages {
    stage('Checkout') {
      steps {
        git branch: 'main', url: 'https://github.com/chakravarthigit/cara-frontend.git'
      }
    }

    stage('Install Yarn & Dependencies') {
      steps {
        sh 'npm install -g yarn'
        sh 'yarn install'
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
