pipeline {
    agent any 
    stages {
        stage('Build') { 
            steps {
                echo 'Building'
                sh 'npm install'
                sh 'npm run build'
            }
            post {
                failure {
                    emailext
                        body: "${currentBuild.currentResult}: Job ${env.JOB_NAME} build ${env.BUILD_NUMBER}",
                        to: 'kin.baryczka@gmail.com',
                        subject: "Build failed in Jenkins Job ${env.JOB_NAME}"
                }
                success {
                    emailext
                        body: "${currentBuild.currentResult}: Job ${env.JOB_NAME} build ${env.BUILD_NUMBER}",
                        to: 'kin.baryczka@gmail.com',
                        subject: "Successful build in Jenkins Job ${env.JOB_NAME}"
                }
            }
        }
        stage('Test') { 
            steps {
                echo 'Testing'
                sh 'npm run test'
            }
            post {
                failure {
                    emailext
                        body: "${currentBuild.currentResult}: Job ${env.JOB_NAME} build ${env.BUILD_NUMBER}",
                        to: 'kin.baryczka@gmail.com',
                        subject: "Tests failed in Jenkins Job ${env.JOB_NAME}"
                }
                success {
                    emailext
                        body: "${currentBuild.currentResult}: Job ${env.JOB_NAME} build ${env.BUILD_NUMBER}",
                        to: 'kin.baryczka@gmail.com',
                        subject: "Successful tests in Jenkins Job ${env.JOB_NAME}"
                }
            }
        }
        stage('Deploy') { 
            steps {
                echo 'Deploying'
            }
        }
    }
    post {
        failure {
            emailext attachLog: true,
                body: "${currentBuild.currentResult}: Job ${env.JOB_NAME} build ${env.BUILD_NUMBER}",
                to: 'kin.baryczka@gmail.com',
                subject: "Build failed in Jenkins ${currentBuild.currentResult}: Job ${env.JOB_NAME}"
        }
        success {
            emailext attachLog: true,
                body: "${currentBuild.currentResult}: Job ${env.JOB_NAME} build ${env.BUILD_NUMBER}",
                to: 'kin.baryczka@gmail.com',
                subject: "Successful build in Jenkins ${currentBuild.currentResult}: Job ${env.JOB_NAME}"
        }
    }
}
