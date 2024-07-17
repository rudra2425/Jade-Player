pipeline {
    agent any  // Executes this pipeline on any available agent

    environment {
        ANDROID_HOME = " /usr/lib/android-sdk/"  // Path to your Android SDK
        PATH = "${ANDROID_HOME}/tools/bin:${ANDROID_HOME}/platform-tools:${PATH}"
    }

    stages {
        stage('Checkout') {
            steps {
                // Checkout your Git repository
                checkout scmGit(branches: [[name: '*/main']], extensions: [], userRemoteConfigs: [[credentialsId: 'github', url: 'https://github.com/rudra2425/Jade-Player.git']])
            }
        }

        stage('Build') {
            steps {
                // Set up the Android SDK licenses
                sh 'yes | sdkmanager --licenses'

                // Build your Android project
                sh './gradlew clean assembleDebug'
            }
        }
        stage('Accept SDK Licenses') {
            steps {
                // Accept Android SDK licenses
                sh '/usr/lib/android-sdk/tools/bin/sdkmanager --licenses'
            }
        }

        stage('Unit Tests') {
            steps {
                // Run unit tests if applicable
                sh './gradlew test'
            }
        }

        stage('UI Tests') {
            steps {
                // Run UI tests if applicable
                sh './gradlew connectedAndroidTest'
            }
        }

        stage('Deploy APK') {
            steps {
                // Example: Deploy APK to Firebase App Distribution
                // Replace with your deployment steps if needed
                sh './gradlew assembleRelease'  // Example command, adjust as per your needs
            }
        }
    }

    post {
        always {
            // Clean up workspace or any post-build tasks
            cleanWs()
        }
    }
}
