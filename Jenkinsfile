pipeline {
  agent any

  tools {
    nodejs 'Node 18'  // Make sure this matches your NodeJS installation name in Jenkins Global Tool Configuration
  }

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
