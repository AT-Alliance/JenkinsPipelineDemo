pipeline {
    agent any

    stages {
        stage('RestoreNuget') { // Restore nuget
            steps {
                script {
					try {
					    bat '"%WORKSPACE%\\build\\nuget.exe" restore "%WORKSPACE%\\GCRADC.sln"'
						println "Restore GCRADC.sln successfull!!"
					} catch (err){
						println "Restore GCRADC.sln failed: ${err}"
					}
				}
            }
        }
		stage('BuildSolution') { // 
            steps {
                script {
					try {
					    // Build solution step
					    powershell 'C:\\\'Program Files (x86)\'\\\'Microsoft Visual Studio\'\\2019\\Professional\\MSBuild\\Current\\Bin\\MSBuild.exe .\\GCRADC.sln /p:Configuration=Release'
						println "Build GCRADC.sln successfull!!"
					} catch (err){
						println "Build GCRADC.sln failed: ${err}"
					}
				}
            }
        }
	}
}
