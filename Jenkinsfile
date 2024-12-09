pipeline{

    agent any

    parameters {
        choice choices: ['chrome', 'firefox'], description: 'Select the browser', name: 'BROWSER'
    }

    stages{

        stage('Start Grid'){
            steps{
                bat "docker-compose -f gridStart.yaml up --scale ${params.BROWSER}=1 -d"
            }
        }

        stage('Run Test'){
            steps{
                bat "docker-compose -f test_suites.yaml up --pull=always"
                script {
                    if(fileExists('output/flightApplication/testng-failed.xml') || fileExists('output/vendorApplication/testng-failed.xml')){
                        error('failed tests found')
                    }
                }
            }
        }

    }

    post {
        always {
            sh "docker-compose -f gridStart.yaml down"
            sh "docker-compose -f test_suites.yaml down"
            archiveArtifacts artifacts: 'C:/Users/manir/eclipse-workspace/dockerPractice/output/flightApplication/emailable-report.html', followSymlinks: false
            archiveArtifacts artifacts: 'C:/Users/manir/eclipse-workspace/dockerPractice/output/vendorApplication/emailable-report.html', followSymlinks: false
        }
    }

}