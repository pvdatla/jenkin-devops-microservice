// Scripted Pipeline
// Declarative Pipeline
pipeline {
	//agent any
	agent { docker {image 'maven:3.9.9'} }
	stages {
		stage('Build') {
			steps {
				sh 'mvn --version'
				echo "Build"

			}
		}
		stage('Test') {
			steps {
				echo "Test"

			}
		}
		stage('Integration Test') {
			steps {
				echo "Integration Test"

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
