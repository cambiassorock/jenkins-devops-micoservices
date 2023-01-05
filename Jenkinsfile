pipeline { //con pipeline ya toma automatico cada minuto desde jenkins para ejecutar con cada commit en github el pipeline
	//agent any
	agent{ docker {image 'maven:3.6.3'}}
	stages{
		stage('Build') {
			steps{
				echo "mvn --version"
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
		}
		failure{
			echo 'Ejecucion Fallida...'
		}
		changed {
			echo 'Ejecucion Cuando estado cambia...'
		}
	}
}
