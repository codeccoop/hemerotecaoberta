pipeline {
	agent { dockerfile true }
	
	stages {
		stage('Build') {
			steps {
				sh 'node --version'
				// stash includes: './file', name: 'testfile'
            }
        }

		stage('Deploy') {
			when {
            	expression {
                	currentBuild.result == null || currentBuild.result == 'SUCCESS' 
              	}
            }
			environment {
				ID_RSA = credentials('orzopad')
			}
			steps {
				// unstash 'testfile'
				sh 'mkdir -p .ssh && echo ${ID_RSA} > .ssh/id_rsa'
				sh 'ssh orzo@192.168.10.130 "echo $HOSTNAME"'
				// sh 'cat ./file'
			}
		}
    }
}
