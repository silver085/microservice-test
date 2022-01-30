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
		stage('Package'){
			steps {
				sh "mvn package -DskipTests"
			}
		}
		stage('Build docker image'){
			steps {
				// docker build -t fmontesano/microservice-test:$env.BUILD_TAG
				script {
					dockerImage = docker.build("fmontesano/microservice-test:${env.BUILD_TAG}")
				}
			}
		}
		stage('Push docker image'){
			steps {
				script {
				docker.withRegistry('', 'dockerhub'){	
					dockerImage.push();
					dockerImage.push('last');
				}
				}
			}
		}
		stage('Run the image'){
			steps {
				script {
					docker.image(dockerImage).withRun('-p 8000:8000') {}
				}
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