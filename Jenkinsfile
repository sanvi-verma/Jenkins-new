pipeline {
    agent any   // Use any available Jenkins agent

    environment {
        REPO_URL = 'https://github.com/yourusername/your-repo.git'
        BRANCH = 'main'
        BUILD_START_TIME = ''
        BUILD_END_TIME = ''
    }

    options {
        timestamps()  // Adds timestamps to logs
    }

    stages {
        // 📌 Stage 1: Checkout Source Code
        stage('Checkout Source Code') {
            steps {
                script {
                    env.BUILD_START_TIME = new Date().format("yyyy-MM-dd HH:mm:ss", TimeZone.getTimeZone('UTC'))
                    echo "🚀 Checking out source code from $REPO_URL"

                    checkout scm  // Default SCM checkout

                    // Extract Git Metadata
                    def gitCommit = sh(script: "git rev-parse HEAD", returnStdout: true).trim()
                    def gitBranch = sh(script: "git rev-parse --abbrev-ref HEAD", returnStdout: true).trim()
                    def lastCommitMessage = sh(script: "git log -1 --pretty=%B", returnStdout: true).trim()

                    echo "📌 Git Branch: ${gitBranch}"
                    echo "📌 Latest Commit Hash: ${gitCommit}"
                    echo "📌 Last Commit Message: ${lastCommitMessage}"
                }
            }
        }

        // 📌 Stage 2: Build the Application
        stage('Build Application') {
            steps {
                script {
                    try {
                        echo "🔨 Building the application..."
                        sh 'echo "Simulating build process..."'  // Replace with actual build command

                        currentBuild.result = "SUCCESS"  // Simulate success
                    } catch (Exception e) {
                        currentBuild.result = "FAILURE"
                        error("🚨 Build failed")
                    }
                }
            }
        }

        // 📌 Stage 3: Fetch Tests from Git
        stage('Get Tests from Git') {
            steps {
                script {
                    echo "🛠️ Fetching test scripts from Git..."
                    sh 'echo "Simulating fetching test scripts..."'  // Replace with actual fetch command
                }
            }
        }

        // 📌 Stage 4: Execute Tests
        stage('Execute Tests') {
            steps {
                script {
                    try {
                        echo "✅ Running tests..."
                        sh 'echo "Simulating test execution..."'  // Replace with actual test command

                        currentBuild.result = "SUCCESS"
                    } catch (Exception e) {
                        currentBuild.result = "FAILURE"
                        error("🚨 Test execution failed")
                    }
                }
            }
        }

        // 📌 Stage 5: Deploy Application
        stage('Deploy Application') {
            steps {
                script {
                    try {
                        echo "📦 Deploying application..."
                        sh 'echo "Simulating deployment..."'  // Replace with actual deployment command

                        currentBuild.result = "SUCCESS"
                    } catch (Exception e) {
                        currentBuild.result = "FAILURE"
                        error("🚨 Deployment failed")
                    }
                }
            }
        }
    }

    // 📌 Post-build Actions (Capture Pipeline Data)
    post {
        always {
            script {
                env.BUILD_END_TIME = new Date().format("yyyy-MM-dd HH:mm:ss", TimeZone.getTimeZone('UTC'))
                def buildData = [
                    jobName: env.JOB_NAME,
                    buildNumber: env.BUILD_NUMBER,
                    startTime: env.BUILD_START_TIME,
                    endTime: env.BUILD_END_TIME,
                    buildResult: currentBuild.result,
                    executedBy: env.BUILD_USER
                ]

                echo "📊 Pipeline Execution Summary: ${buildData}"
            }
        }
    }
}
