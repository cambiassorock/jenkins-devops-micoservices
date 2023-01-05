pipeline { //con pipeline ya toma automatico cada minuto desde jenkins para ejecutar con cada commit en github el pipeline
	//agent any
	agent{ docker {image 'node:13.8'}}
	stages{
		stage('Build') {
			steps{
				//sh "mvn --version"
				sh "node --version"
				echo "Paso 1. Build"
				echo "Paso 2. Build"
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
