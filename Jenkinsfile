pipeline {
  agent any

  stages {
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
    stage('Run Tests') {
      steps {
        sh 'yarn test'
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
