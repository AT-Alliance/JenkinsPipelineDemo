pipeline {
    agent any

    stages {
		stage('Checkout') {
            steps {
				echo "Hello Mr. ${env.BUILD_DISPLAY_NAME}.."
				echo "Jenkins url ==> ${JENKINS_URL}"
				echo "Jenkins revision ==> ${env.SVN_REVISION}"
				bat 'whoami'
                script {
					try {
						sh "svn status -u -v wc"
					} catch (err){
						println "svn checkout failed: ${err}"
					}
				}
            }
        }
		stage('Execution en parallele') {
			steps {
				parallel (
					Build : {
						bat "echo Running ${env.BUILD_ID} on ${env.JENKINS_URL}"
						bat 'echo Building..'
					},
					Testing : {
						bat 'echo Testing..'
					},
					Deploy : {
						bat 'echo Deploying....'
					}
				)
			}
		}
    }
    post {
        success {
            emailext (
                to: 'atchezeu@groupealliance.eu',
                subject: "[BuildResult][${currentBuild.currentResult}] - Job '${env.JOB_NAME}' (${env.BUILD_NUMBER})",
                body: '''${SCRIPT, template="email.groovy.template"}''',
                attachLog: true
            )
        }
        failure {
            emailext (
                to: 'atchezeu@groupealliance.eu',
                subject: "[BuildResult][${currentBuild.currentResult}] - Job '${env.JOB_NAME}' (${env.BUILD_NUMBER})",
                body: '''${SCRIPT, template="email.groovy.template"}''',
                attachLog: true
            )
       }
	}
}
