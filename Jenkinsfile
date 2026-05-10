pipeline{
	agent any
	
	environment{
	LANG = 'en_US.UTF-8'
	LC_ALL = "en_US.UTF-8"
	}

	tools{
		maven 'Maven'
	}
	
	stages{
		stage('Checkout'){
			steps{
				git branch : 'main', url : 'https://github.com/Someesvaar/practice_ansible.git'
			}
		}
		
		stage('Buid'){
			steps{
				sh 'mvn clean package'
			}
		}
		
		stage('archive'){
			steps{
				archiveArtifacts artifacts: 'target/*.war', fingerprint:true
			}
		}
		
		stage('Deploy'){
			steps{
				sh 'ansible-playbook ansible/playbook.yml -i hosts.ini'
			}
		}
	}
	
	post{
		success {
			echo "Build Successful"
		}
		failure{
			echo "Build Failure" 
		}
	}
}
