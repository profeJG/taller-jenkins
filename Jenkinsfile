pipeline{
	agent any
	stages{
		stage('Obtener el repositorio'){
			steps{
				echo "git clone"
				git branch: 'main', url: 'https://github.com/profeJG/taller-jenkins.git'				
			}
		}
		stage('Generar documentación'){
			steps{
				echo "doxygen"
				echo "ZIP"
				sh "doxygen; zip documentacion.zip -r html/*"
			}
		}

		stage('Análisis estático'){
                        steps{
                                echo "Análisis estático con cppcheck"
                                sh "if [ ! -d reports/cppcheck ] ; then mkdir -p reports/cppcheck ; fi"
				echo "Creada carpeta reports/cppcheck"
				sh "make cppcheck-xml"
				// Analizamos el resultado
				recordIssues(tools: [cppCheck(pattern: 'reports/cppcheck/*.xml')])
                        }
                }
	}
	post{
		success{
			echo "Publicar HTML"
			publishHTML([allowMissing: false, alwaysLinkToLastBuild: false, keepAll: false, reportDir: 'html', reportFiles: 'files.html', reportName: 'HTML Report', reportTitles: '', useWrapperFileDirectly: true])
			// archive 'documentacion.zip'
			echo "Adjuntando ficheros .zip"
			archiveArtifacts artifacts: '**/*.zip'						
		}
	}
}
