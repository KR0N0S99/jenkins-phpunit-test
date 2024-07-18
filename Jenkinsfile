pipeline {
    agent any
    stages {
        stage('Build') {
            steps {
                script {
                    docker.image('composer:latest').inside {
                        sh 'composer install'
                    }
                }
            }
        }
        stage('Test') {
            steps {
                script {
                    docker.image('composer:latest').inside {
                        sh './vendor/bin/phpunit --log-junit logs/unitreport.xml -c tests/phpunit.xml tests'
                    }
                }
            }
        }
    }
    post {
        always {
            junit 'logs/unitreport.xml'
        }
    }
}
