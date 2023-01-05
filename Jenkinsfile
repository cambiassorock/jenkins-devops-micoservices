pipeline { //con pipeline ya toma automatico cada minuto desde jenkins para ejecutar con cada commit en github el pipeline
	agent any
	//agent{ docker {image 'node:13.8'}}
	environment {
		dockerHome = tool 'myDocker'
		mavenHome = tool 'myMaven'
		PATH ="$dockerHome/bin:$PATH:$mavenHome/bin:$PATH"
	}
	
	stages{
		stage('Build') {
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
		stage('Test') {
			steps{
				echo "Paso 1. Test"
				echo "Paso 2. Test"
			}
		}
		stage('Integration Test') {
			steps{
				echo "Paso 1. Integration Test"
				echo "Paso 2. Integration Test"
				echo "Paso 3. Integration Test"
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
