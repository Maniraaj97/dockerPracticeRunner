pipeline{

    agent any

    stages{

        stage('Turn on grid'){
            steps{
                bat 'docker-compose -f grid.yaml up -d'
            }
        }

        stage('Run Test'){
            steps{
                bat 'docker-compose -f test_suites.yaml up'
            }
        }
		
		post{
		    
		    always{
		        
		        bat 'docker-compose -f grid.yaml down'
		        bat 'docker-compose -f test_suites.yaml down'
		    }

		}

  
    }


}