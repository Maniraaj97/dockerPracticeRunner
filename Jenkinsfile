pipeline {

    agent any

    stages {

        stage('Turn on grid') {
            steps {
                bat 'docker-compose -f gridStart.yaml up -d'
            }
        }

        stage('Run Test') {
            steps {
                bat 'docker-compose -f test_suites.yaml up'
            }
        }
    }

    post {
        always {
            bat 'docker-compose -f gridStart.yaml down'
            bat 'docker-compose -f test_suites.yaml down'
        }
    }
}
