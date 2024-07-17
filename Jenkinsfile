pipeline {
    agent any

    environment {
        ANDROID_HOME = "/usr/lib/android-sdk"
        PATH = "${ANDROID_HOME}/cmdline-tools/tools/bin:${ANDROID_HOME}/platform-tools:${env.PATH}"
    }

    stages {
        stage('Checkout') {
            steps {
                // Checkout your Git repository
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
                // Change directory to your project root where gradlew is located
                dir('path/to/your/project/root') {
                    // Make sure gradlew is executable
                    sh 'chmod +x gradlew'
                }
            }
        }
        stage('Build') {
            steps {
                // Execute Gradle build using the Gradle Wrapper
                dir('path/to/your/project/root') {
                    sh './gradlew clean assembleDebug --stacktrace'
                }
            }
        }
        // Add more stages as needed (Unit Tests, UI Tests, Deploy APK)
    }

    post {
        always {
            cleanWs()
        }
    }
}
