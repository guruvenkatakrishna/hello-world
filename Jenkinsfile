pipeline {
	agent any 	
	environment{
		TOMCAT_USER="ec2-user"
		TOMCAT_HOST="172.31.43.219"
		TOMCAT_PATH="/home/ec2-user/tomcat/webapps"
	}
	stages {
		stage('Checkout') {
			steps {
				echo 'Checkout completed'
				git branch: 'master', url: 'https://github.com/guruvenkatakrishna/hello-world.git'
			}
		}
		stage('test') {
			steps {
				echo 'This is test on code.Assume it is tested'
			}
		}
		stage('Build') {
			steps {
				sh 'mvn clean install'
			}
		}
		stage('Deploy') {
			steps {
			sshagent(['java']) {
				echo 'Deploying into environment'
				sh'rsync -avz -e ssh /var/lib/jenkins/workspace/tomcat/webapp/target/*.war ubuntu@172.31.1.14/home/ubuntu/tomcat/webapps'
			}
			}
		}
	}
}
