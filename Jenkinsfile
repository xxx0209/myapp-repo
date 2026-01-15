pipeline {
	agent any

    environment {
        REGISTRY = "192.168.56.101:5000"
        IMAGE = "myapp:1.0"
    }

    stages {
        stage('Checkout') {
            steps {                
				// GitHub에서 소스코드 clone
                git branch: 'main',
                    url: 'git@github.com:xxx0209/myapp-repo.git',
                    credentialsId: 'github-ssh'  // 여기에 Jenkins Credential ID
            }
        }

        stage('Build Image') {
            steps {
                sh 'docker build -t $REGISTRY/$IMAGE .'
            }
        }

        stage('Push Registry') {
            steps {
                sh 'docker push $REGISTRY/$IMAGE'
            }
        }

        stage('Deploy to K8s') {
            steps {
                sh 'ssh vm2 kubectl set image deployment/myapp myapp=$REGISTRY/$IMAGE'
            }
        }
    }
}