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
    // test stage removed
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
    }  // <-- Make sure no extra closing brace here
  }  // end stages

} // end pipeline
