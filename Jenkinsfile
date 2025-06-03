pipeline {
  agent any

  tools {
    nodejs 'Node 18'  // Name must match Jenkins NodeJS installation config
  }

  environment {
    ANDROID_HOME = '/opt/android-sdk'
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
        // Use the 'node' and 'yarn' binaries installed by NodeJS plugin
        sh 'node -v'
        sh 'npm install -g yarn'    // Install yarn globally in pipeline (if not pre-installed)
        sh 'yarn install'
      }
    }

    stage('Configure Android SDK') {
      steps {
        sh '''
          echo "sdk.dir=${ANDROID_HOME}" > android/local.properties
          cat android/local.properties
        '''
      }
    }

    stage('Build Android') {
      steps {
        dir('android') {
          sh '''
            export ANDROID_HOME=${ANDROID_HOME}
            export PATH=$ANDROID_HOME/tools:$ANDROID_HOME/tools/bin:$ANDROID_HOME/platform-tools:$PATH
            ./gradlew clean assembleRelease --stacktrace
          '''
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
