pipeline {
    agent any

    stages {
        stage('Checkout') {
            steps {
                // Obtiene el código del repositorio
                git 'https://github.com/dsiyarp/desafio11.git'
            }
        }
        
        stage('Verificar Archivos') {
            steps {
                // Lista los archivos en el workspace
                sh 'ls -la'
            }
        }
        
        stage('Preparar Despliegue') {
            steps {
                // Verifica que el archivo index.html existe
                sh 'test -f index.html'
            }
        }
        
        stage('Desplegar a Servidores') {
            steps {
                echo 'Preparado para desplegar a los servidores web'
                // Aquí añadiremos después la integración con Ansible
            }
        }
    }
    
    post {
        success {
            echo '¡Pipeline ejecutado con éxito!'
        }
        failure {
            echo 'El pipeline ha fallado'
        }
    }
}