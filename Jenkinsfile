pipeline{
    agent any
    tools{
        nodejs 'NODE-JS'
    }
    stages{
        stage('Clone Repo'){
            steps{
                git 'https://github.com/NelsonOngany/gallery.git'
            }
        }
        stage('Build'){
            steps{
                sh 'npm install'
            }
        }
        stage('Test'){
            steps{
                sh 'npm test'
            }
        }
         stage('Deploy to Heroku'){
            steps{
                withCredentials([usernameColonPassword(credentialsId:'heroku', variable:'HEROKU_CREDENTIALS')]){
                    sh 'git push https://${HEROKU_CREDENTIALS}@git.heroku.com/intense-scrubland-40782.git master'
                }
            }
        }
    }
    post{
        always{
            emailext attachLog: true, body: 'Email from Jenkins', subject: '$PROJECT_NAME - Build # $BUILD_NUMBER - $BUILD_STATUS: ', to: 'nharold039@gmail.com'
            slackSend channel:'jenkins', color: 'good', message: "Node Gallery Pipeline Message- ${currentBuild.currentResult}  ${env.JOB_NAME} ${env.BUILD_NUMBER} ${BUILD_URL}"
        }
        
    }
}