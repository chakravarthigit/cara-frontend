pipeline {
  agent any

  tools {
    nodejs 'Node 18'
  }

  environment {
    ANDROID_HOME = '/opt/android-sdk'  // Change to your SDK location
    PATH = "${ANDROID_HOME}/tools:${ANDROID_HOME}/tools/bin:${ANDROID_HOME}/platform-tools:${env.PATH}"
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
