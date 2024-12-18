pipeline {
    agent any
    
    options {
        skipDefaultCheckout(true) // Evitamos el checkout por defecto
    }

    stages {
        stage('Checkout') {
            steps {
                // Limpiamos el workspace
                cleanWs()
                // Checkout específico de la rama main
                checkout([
                    $class: 'GitSCM',
                    branches: [[name: '*/main']],
                    extensions: [],
                    userRemoteConfigs: [[
                        url: 'https://github.com/dsiyarp/desafio11.git'
                    ]]
                ])
            }
        }
        
        stage('Verificar Archivos') {
            steps {
                sh '''
                    echo "Contenido del directorio:"
                    ls -la
                '''
            }
        }
        
        stage('Preparar Despliegue') {
            steps {
                script {
                    if (fileExists('index.html')) {
                        echo "index.html encontrado"
                    } else {
                        error "index.html no encontrado en el repositorio"
                    }
                }
            }
        }
        
        stage('Desplegar a Servidores') {
            steps {
                echo 'Preparado para desplegar a los servidores web'
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
        always {
            echo 'Pipeline finalizado'
        }
    }
}