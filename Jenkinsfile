pipeline {
    agent any
    stages {
        stage('Application docker build') {
            steps {
                withCredentials([usernamePassword(credentialsId: 'harbor-auth', variable: 'HARBOR-AUTH')]) {
                    script{
                        tool name: 'docker'
                        docker.build('lab-test:latest')
                        docker.withServer('https://harbor.dev.afsmtddso.com', '$HARBOR-AUTH') {
                            docker.image('lab-test:latest').push('latest')
                        }
                    }
                }
            }
        }
        stage('Database docker build') {
            steps {
                withCredentials([usernamePassword(credentialsId: 'harbor-auth', variable: 'HARBOR-AUTH')]) {
                    script{
                        tool name: 'docker'
                        docker.build('db-test:latest', '-f dbDockerfile .')
                        docker.withServer('https://harbor.dev.afsmtddso.com', '$HARBOR-AUTH') {
                            docker.image('db-test:latest').push('latest')
                        }
                    }
                }
            }
        }
    }
}