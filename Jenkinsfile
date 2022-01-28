pipeline {
	agent any
	stages {
		stage('Build'){
			steps{
				echo "Started build stage"
			}
		}
		stage('Test'){
			steps{
				echo "Started test stage"
			}
		}
		stage('Integration Test'){
			steps{
				echo "Started Integration test stage"
			}
		}
	} 
	
	post {
		always {
			echo "Pipeline completed"
		}
		success {
			echo "Succesfully!"
		}
		failure {
			echo "Problems happened."
		}
	}
}