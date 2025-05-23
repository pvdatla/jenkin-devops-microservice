// Scripted Pipeline
// Declarative Pipeline
pipeline {
	agent any
	//agent { docker {image 'maven:3.9.9'} }
	//agent { docker {image 'node:lts-jod'} }
	environment {
		dockerHome = tool 'myDocker'
		mavenHome = tool 'myMaven'
		path = "$dockerHome/bin:$mavenHome/bin:$PATH"
	}
	stages {
		stage('Checkout') {
			steps {
				sh 'mvn --version'
				sh 'docker version'
				echo "Build"
				echo "PATH - $PATH"
				echo "BUILD_NUMBER - $env.BUILD_NUMBER"
				echo "BUILD_ID - $env.BUILD_ID"
				echo "JOB_NAME - $env.JOB_NAME"
				echo "BUILD_TAG - $env.BUILD_TAG"
				echo "BUILD_URL - $env.BUILD_URL"
			}
		}

		stage('Compile') {
			steps {
				sh "mvn clean compile"
			}
		}

		stage('Test') {
			steps {
				sh "mvn test"

			}
		}

		stage('Integration Test') {
			steps {
				sh "mvn failsafe:integration-test failsafe:verify"

			}
		}

		stage('Package') {
			steps {
				sh "mvn package -DskipTests"

			}
		}

		stage('Build Docker Image') {
			steps {
				//sh " docker build -t pradeepregistry/currency-exchange-devops:$env.BUILD_TAG"
				// this is typical declarative version
				script {
					dockerImage = docker.build("pradeepregistry/currency-exchange-devops:${env.BUILD_TAG}")
				}

			}
		}

		stage('Push Docker Image') {
			steps {
				script {
					docker.withRegistry('', 'dockerhub') {
					dockerImage.push();
					dockerImage.push('latest');
					}
				}
				
			}
		}
	}
	post {
		always {
			echo 'Im awesome, I run always'
		}
		success {
		    echo 'I run when you are success' 
		}
		failure {
			echo 'I run when you fail'
		}
	}
	
}
