pipeline {
  agent {
    docker {
      image 'node:18' // Official Node.js image with npm and yarn
      args '-u root'  // Allows installing global packages
    }
  }

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
