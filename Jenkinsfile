pipeline {
    agent any

    parameters {
        string(name: 'GIT_URL', defaultValue: 'https://github.com/harshada-zurunge/Maven-based-Java-Project.git', description: 'Git repository URL')
        string(name: 'MAVEN_GOALS', defaultValue: 'clean install', description: 'Maven goals to execute')
        booleanParam(name: 'RUN_TESTS', defaultValue: true, description: 'Run tests during the build')
    }

    stages {
        stage('Checkout Code') {
            steps {
                script {
                    // Checkout code from the specified Git repository
                    checkout([$class: 'GitSCM', branches: [[name: '*/main']], doGenerateSubmoduleConfigurations: false, extensions: [], submoduleCfg: [], userRemoteConfigs: [[url: params.GIT_URL]]])
                }
            }
        }

        stage('Build') {
            steps {
                // Perform Maven build with specified goals
                script {
                    def mavenCmd = "mvn ${params.MAVEN_GOALS}"
                    if (params.RUN_TESTS == false) {
                        mavenCmd += ' -DskipTests'
                    }
                    sh mavenCmd
                }
            }
        }

        stage('Test') {
            when {
                expression { params.RUN_TESTS == true }
            }
            steps {
                // Run tests (you can customize this based on your testing framework)
                script {
                    sh 'echo "Running tests..."'
                }
            }
        }

        stage('Deploy') {
            steps {
                // Simulate deployment (you can replace this with actual deployment steps)
                sh 'echo "Deploying the application..."'
            }
        }
    }

    post {
        success {
            // Notify success
            echo 'Pipeline succeeded! Your application is ready for deployment.'
        }

        failure {
            // Notify failure
            echo 'Pipeline failed! Check the build and test results.'
        }
    }
}
