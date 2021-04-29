pipeline {
    agent any 
    stages {
        stage('Build') { 
            steps {
                echo 'Building'
                sh 'npm install'
                sh 'npm run build'
            }
        }
        stage('Test') { 
            steps {
                echo 'Testing'
                sh 'npm run test'
            }
        }
        stage('Deploy') { 
            steps {
                echo 'Deploying'
            }
        }
    }
    environment {
        EMAIL_TO = 'kin.baryczka@gmail.com'
    }
    post {
        failure {
            emailext body: 'Check console output at $BUILD_URL to view the results. \n\n ${CHANGES} \n\n -------------------------------------------------- \n${BUILD_LOG, maxLines=100, escapeHtml=false}', 
                to: "${EMAIL_TO}", 
                subject: 'Build failed in Jenkins: $PROJECT_NAME - #$BUILD_NUMBER'
        }
        success {
            emailext body: 'Check console output at $BUILD_URL to view the results. \n\n ${CHANGES} \n\n -------------------------------------------------- \n${BUILD_LOG, maxLines=100, escapeHtml=false}', 
                to: "${EMAIL_TO}",
                subject: 'Successful build in Jenkins: $PROJECT_NAME - #$BUILD_NUMBER'
        }
    }
}
