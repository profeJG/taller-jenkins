pipeline{
	agent any
	stages{
		stage('Obtener el repositorio'){
			steps{
				echo "git clone"
			}
		}
		stage('Generar documentación'){
			steps{
				echo "doxygen"
				echo "ZIP"
			}
		}
	}
	post{
		success{
			echo "Publicar HTML"
		}
	}
}
