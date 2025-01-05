pipeline {
    agent { label 'lxd' }  // Указание метки агента

    environment {
        HOME = '/root'  // Установка переменной окружения HOME
    }
    
    stages {
        stage('Checkout') {
            steps {
                script {
                    git branch: "${env.BRANCH_NAME}", url: 'https://github.com/Torrmund/ansible_vector_role.git'
                }
            }
        }
        
        stage('Setup Environment') {
            steps {
                script {
                    // Удаление старого окружения
                    sh 'rm -rf env/'
                    // Создание нового виртуального окружения
                    sh 'virtualenv --python=/usr/bin/python3 env'
                }
            }
        }
        
        stage('Install Requirements') {
            steps {
                script {
                    // Активация виртуального окружения и установка зависимостей
                    sh '''#!/bin/bash
                    source env/bin/activate
                    pip install -r requirements.txt
                    deactivate
                    '''
                }
            }
        }
        
        stage('Run Molecule Tests') {
            steps {
                script {
                    // Запуск тестов Molecule
                    sh '''#!/bin/bash
                    source env/bin/activate
                    molecule test
                    deactivate
                    '''
                }
            }
        }
        
        stage('Cleanup') {
            steps {
                // Удаление окружения после завершения
                sh 'rm -rf env/'
            }
        }
    }

    post {
        always {
            // Дополнительные действия после завершения пайплайна (уведомление о завершении pipeline)
            echo 'Pipeline completed.'
        }
        failure {
            // Действия в случае ошибки
            echo 'Pipeline failed!'
        }
    }
}