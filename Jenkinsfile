pipeline {
	agent any
	stages {
		stage('Build'){
			steps{
				echo "Build step"
				echo "$PATH"
				echo "BUILD_NUMBER -$env.BUILD_NUMBER"
				echo "BUILD_ID - $env.BUILD_ID"
				echo "JOB NAME - $env.JOB_NAME"
				echo "BUILD TAG - $env.BUILD_TAG"
				echo "BUILD URL - $env.BUILD_URL"
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