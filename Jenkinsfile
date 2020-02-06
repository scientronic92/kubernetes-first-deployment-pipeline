pipeline {
    agent any
    stages {
        stage('install dependencies') {
            steps {
		sh "pip install venv"
		sh "python3 -m venv ~/.devops"
		sh "pip install --upgrade pip"
		sh "pip install -r requirements.txt"
            }
        }
        stage('Lint python') {
            steps {
                sh "pylint --disable=R,C,W1203 app.py"
            }
        }
        stage('build docker') {
            steps {
		sh "./run_docker.sh"
            }
        }
        stage('upload docker') {
            steps {
		sh "./upload_docker.sh"
            }
        }
        stage('run kops') {
            steps {
		sh "./run_kops.sh"
            }
	}
        stage('run kubernetes') {
            steps {
		sh "./run_kubernetes.sh"
            }
        }
    }
}
