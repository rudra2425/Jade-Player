pipeline {
    agent any
    
    environment {
        ANDROID_HOME = "/usr/lib/android-sdk"
        PATH = "${ANDROID_HOME}/cmdline-tools/tools/bin:${ANDROID_HOME}/platform-tools:${env.PATH}"
    }

    stages {
        stage('Checkout') {
            steps {
                checkout scmGit(branches: [[name: '*/main']], extensions: [], userRemoteConfigs: [[credentialsId: 'github', url: 'https://github.com/rudra2425/Jade-Player.git']])
            }
        }
        stage('Accept SDK Licenses') {
            steps {
                sh '/usr/lib/android-sdk/cmdline-tools/tools/bin/sdkmanager --licenses < /dev/null'
            }
        }
        stage('Prepare Gradle') {
            steps {
                sh 'chmod +x ./gradlew'
            }
        }
        stage('Build') {
            steps {
                sh './gradlew clean assembleDebug --stacktrace'
            }
        }
        stage('Unit Tests') {
            steps {
                sh './gradlew test --stacktrace'
            }
        }
        stage('UI Tests') {
            steps {
                sh './gradlew connectedAndroidTest --stacktrace'
            }
        }
        stage('Deploy APK') {
            steps {
                sh './gradlew assembleRelease --stacktrace'  // Adjust as per your deployment needs
            }
        }
    }

    post {
        always {
            cleanWs()
        }
    }
}
