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
                bat 'C:\\Users\\Usuario\\AppData\\Local\\Programs\\Python\\Python311\\Scripts\\pip.exe install -r mlops\\requirements.txt'
            }
        }

        stage('Entrenar modelo') {
            steps {
                bat 'python mlops/train_model.py'
            }
        }

        stage('Desplegar API') {
            steps {
                bat 'start /b uvicorn mlops.api:app --host 0.0.0.0 --port 8000'
            }
        }
    }
}
