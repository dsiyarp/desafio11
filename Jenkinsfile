pipeline {
    agent any
    
    environment {
        ANSIBLE_HOST = '172.21.238.10'
        ANSIBLE_USER = 'ubuntu'
        GITHUB_REPO = 'https://github.com/dsiyarp/desafio11.git'
    }

    stages {
        stage('Checkout') {
            steps {
                cleanWs()
                git branch: 'main', url: env.GITHUB_REPO
            }
        }
        
        stage('Preparar Ansible') {
            steps {
                script {
                    // Crear directorio en el controlador Ansible
                    sh """
                        ssh ${ANSIBLE_USER}@${ANSIBLE_HOST} '
                            mkdir -p ~/ansible-deploy
                        '
                    """
                    
                    // Copiar archivos al controlador Ansible
                    sh """
                        scp -r * ${ANSIBLE_USER}@${ANSIBLE_HOST}:~/ansible-deploy/
                    """
                }
            }
        }
        
        stage('Ejecutar Ansible Playbook') {
            steps {
                script {
                    sh """
                        ssh ${ANSIBLE_USER}@${ANSIBLE_HOST} '
                            cd ~/ansible-deploy && \
                            ansible-playbook -i inventory.ini deploy-website.yml
                        '
                    """
                }
            }
        }
        
        stage('Verificar Despliegue') {
            steps {
                script {
                    // Verificar que ambos servidores responden
                    sh '''
                        curl -f http://172.21.239.235 || exit 1
                        curl -f http://172.21.225.152 || exit 1
                    '''
                }
            }
        }
    }
    
    post {
        success {
            echo 'Pipeline ejecutado exitosamente'
        }
        failure {
            echo 'El pipeline ha fallado'
        }
        always {
            cleanWs()
        }
    }
}