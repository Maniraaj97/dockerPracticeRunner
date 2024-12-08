pipeline{

    agent any

    stages{

        stage('Run Test'){
            steps{
                bat 'docker-compose up'
            }
        }

        stage('Turn off Grid'){
            steps{
                bat 'docker-compose down'
            }
        }

  
    }


}