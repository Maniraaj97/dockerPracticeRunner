pipeline{

    agent any

    stages{

        stage('Build Jar'){
            steps{
                bat 'mvn clean package -DskipTests'
            }
        }

        stage('Build Image'){
            steps{
                bat 'docker build -t=maniraaj/dockerpractice .'
            }
        }

        stage('Push Image'){
            environment{
                // assuming you have stored the credentials with this name
                DOCKER_HUB = credentials('dockerhub-creds')
            }
            steps{
                bat 'docker login -u %DOCKER_HUB_USR% -p %DOCKER_HUB_PSW%'
                bat 'docker push maniraaj/dockerpractice'
            }
        }

    }

    post {
        always {
            bat 'docker logout'
        }
    }

}