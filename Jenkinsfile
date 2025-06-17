pipeline {
    agent any

    stages {
        stage('Clonar proyecto') {
            steps {
                checkout([$class: 'GitSCM',
                    branches: [[name: '*/main']],
                    userRemoteConfigs: [[
                        url: 'https://github.com/Gusadorey/jenkins-lab.git',
                        credentialsId: 'github-token' // 👈 este es el ID que registraste en Jenkins
                    ]]
                ])
            }
        }

        stage('Instalar dependencias') {
            steps {
                sh 'pip install -r mlops_1/requirements.txt'
            }
        }

        stage('Entrenar modelo') {
            steps {
                sh 'python3 mlops_1/train_model.py'
            }
        }

        stage('Desplegar API') {
            steps {
                sh 'nohup uvicorn mlops_1.api:app --host 0.0.0.0 --port 8000 &'
            }
        }
    }
}
