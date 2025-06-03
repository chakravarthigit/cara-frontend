pipeline {
  agent any

  environment {
    NODE_ENV = 'production'
    ANDROID_HOME = '/opt/android-sdk' // Adjust if needed
    PATH = "$PATH:$ANDROID_HOME/emulator:$ANDROID_HOME/tools:$ANDROID_HOME/platform-tools"
  }

  tools {
    nodejs 'Node 18'  // You must configure this in Jenkins -> Global Tool Configuration
  }

  stages {
    stage('Checkout') {
      steps {
        git 'https://github.com/chakravarthigit/cara-frontend.git'
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
