pipeline {
  agent any

  tools {
    nodejs 'Node 18'  // Make sure this tool is installed and named exactly "Node 18" in Jenkins
  }

  environment {
    ANDROID_HOME = '/opt/android-sdk'  // Change this to your actual SDK path
    PATH = "${ANDROID_HOME}/tools:${ANDROID_HOME}/tools/bin:${ANDROID_HOME}/platform-tools:${env.PATH}"
  }

  stages {
    stage('Checkout') {
      steps {
        // Checkout explicitly main branch
        git branch: 'main', url: 'https://github.com/chakravarthigit/cara-frontend.git'
      }
    }

    stage('Install Dependencies') {
      steps {
        sh 'yarn install'
      }
    }

    stage('Configure Android SDK') {
      steps {
        sh '''
          echo "sdk.dir=${ANDROID_HOME}" > android/local.properties
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
        archiveArtifacts artifacts: 'android/app/build/outputs/apk/release/app-release.apk', fingerprint: true
      }
    }
  }
}
