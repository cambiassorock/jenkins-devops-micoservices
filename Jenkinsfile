pipeline { //con pipeline ya toma automatico cada minuto desde jenkins para ejecutar con cada commit en github el pipeline
	agent any
	//agent{ docker {image 'node:13.8'}}
	environment {
		dockerHome = tool 'myDocker'
		mavenHome = tool 'myMaven'
		PATH ="$dockerHome/bin:$mavenHome/bin:$PATH"
	}
	
	stages{
		stage('Checkout') {
			steps{
				sh "mvn --version"
				sh "docker version"
				//sh "node --version"
				echo "Paso 1. Build"
				echo "PATH - $PATH"
				echo "BUILD_NUMBER - $env.BUILD_NUMBER"
				echo "BUILD_ID - $env.BUILD_ID"
				echo "JOB_NAME - $env.JOB_NAME"
				echo "BUILD_TAG - $env.BUILD_TAG"
				echo "BUILD_URL - $env.BUILD_URL"
			}
		}

		stage('Compile') {
			steps{
				sh "mvn clean compile"
			}
		}

		stage('Test') {
			steps{
				sh "mvn test"
			}
		}

		stage('Integration Test') {
			steps{
				sh "mvn failsafe:integration-test failsafe:verify"
			}
		}

		stage('Package') { //construir el jar
			steps{
				sh "mvn package -DskipTests"
			}
		}
		
		stage('Build Docker Image') //compile la imagen o generela
		{
			steps{
				//forma primitiva de generar imagen del docker hub
				//"docker build -t cambiassorock/currency-exchange-devops:$env.BUILD_TAG"
				script{
					dockerImage = docker.build("cambiassorock/currency-exchange-devops:${env.BUILD_TAG}")
				}
			}
		}

		stage('Push Docker Image') //suba la image
		{
			steps{
				script{
					docker.withRegitry('','DockerHub'){
						dockerImage.push();
						dockerImage.push('latest');
					}
				}
			}
		}
	} 
	post {
		always{
			echo 'Ejecucion normal...'
		}
		success{
			echo 'Ejecucion Exitosa...'
			//mail bcc: '', body: 'Compilación por:  CHANGE_TITLE. Exitosa', cc: '', from: '', replyTo: '', subject: 'Compilacion', to: 'cambiaso_rock@hotmail.com'
		}
		failure{
			echo 'Ejecucion Fallida...'
			//mail bcc: '', body: 'Compilación por:  CHANGE_TITLE. Errores', cc: '', from: '', replyTo: '', subject: 'Compilacion', to: 'cambiaso_rock@hotmail.com'
		}
		changed {
			echo 'Ejecucion Cuando estado cambia...'
		}
	}
}
