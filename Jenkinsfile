pipeline {
    agent any
    stages {
        stage('Build') {
            steps {
                echo 'Running build automation'
                sh './gradlew build --no-daemon'
                archiveArtifacts artifacts: 'dist/trainSchedule.zip'
            }
        }

        stage ('Build Docker Image') {

            sh "docker build -t chanikyamerugu/train-schedule . "
        }

        stage ('Push Docker Image') {

            withCredentials([string(credentialsId: 'dockerhub', variable: 'dockerhub-cred')]) {

                sh "docker push chanikyamerugu/train-schedule -u chanikyamerugu -p {dockerhub-cred}"
            }

        }
    }
}
    
