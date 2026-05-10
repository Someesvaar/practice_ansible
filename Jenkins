pipeline{
	agent any
	
	enviroinment{
	LANG 'en_US.UTF-8'
	LC_ALL "en_US.UTF-8"
	}
	
	stages{
		stage('Checkout'){
			steps{
				git branch : 'master', url : 'https://github.com/Someesvaar/practice_ansible.git'
			}
		}
		
		stage('Package'){
			steps{
				sh 'mvn clean package'
			}
		}
		
		stage('archive'){
			steps{
				archiveArtifacts artifacts: 'target/*.war', fingerprint=true
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
