pipeline {
	agent any
	environment {
		dockerHome = tool "myDocker"
		mavenHome = tool "myMVN"
		PATH = "$mavenHome/bin:$dockerHome/bin:$PATH"
	}
	stages {
		stage('Checkout'){
			steps{
				echo "Build step"
				sh "mvn --version"
				sh "docker version"
				// echo "$PATH"
				// echo "BUILD_NUMBER -$env.BUILD_NUMBER"
				// echo "BUILD_ID - $env.BUILD_ID"
				// echo "JOB NAME - $env.JOB_NAME"
				// echo "BUILD TAG - $env.BUILD_TAG"
				// echo "BUILD URL - $env.BUILD_URL"
			}
		}
		stage('Compile'){
			steps {
				sh "mvn clean compile"
			}

		}
		stage('Test'){
			steps{
				 sh "mvn test"
			}
		}
		stage('Integration Test'){
			steps{
				sh "mvn failsafe:integration-test failsafe:verify"
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