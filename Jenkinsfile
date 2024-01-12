pipeline {
    agent any

    tools {
        nodejs "nodejs"
    }

    stages {
        stage('Install Packages') {
            steps {
                script {
                    sh 'yarn install'
                }
            }
        }

        stage('Run the App') {
            steps {
                script {
                    sh 'yarn start &'
                    sleep 5
                }
            }
        }

        stage('Visit /health route') {
            steps {
                script {
                    sh 'curl http://localhost:3000/health'
                }
            }
        }

        stage('Terminate Deployment') {
            steps {
                script {
                    // This input step will pause the pipeline and wait for user input
                    // before proceeding to the next stage.
                    input "Do you want to terminate the deployment?"
                }
            }
        }

        stage('Cleanup') {
            steps {
                script {
                    sh 'pkill -f "node"'
                }
            }
        }
    }
}
