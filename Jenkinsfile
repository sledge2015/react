pipeline {
    agent any
    
    stages {
        stage('Checkout') {
            steps {
                //  checkout 
                checkout([
                    $class: 'GitSCM',
                    branches: [
                        [
                            name: 'main'
                        ]
                    ],
                    userRemoteConfigs: [
                        [
                            credentialsId: 'Jenkin-2023',
                            url: 'https://gitea.zhiyungb.com/POPS/psa-all.git'
                        ]
                    ]
                ])
            }
        }
        
        stage('Build') {
            steps {
                sh 'npm install yarn -g'
                sh 'yarn install'
                dir('/client/psa-fe') {
                    sh 'yarn dev'
                }
                sh 'cp -R build/ /path/to/output'
            }
        }
        
        stage('Test') {
            steps {
               sh 'node --version'
            }
        }
        
        stage('Deploy') {
            steps {
                sh 'apt-get install -y openssh-client'
        
                sshPublisher(
                    sshPublisherDesc: [
                        configName: 'a4e7a34e-9402-4fd2-8972-212a98aa1248',
                        transfers: [
                            [
                                sourceFiles: '/path/to/output',
                                remoteDirectory: 'C:/Deployment/FE',
                                removePrefix: '/path/to/output',
                                excludes: '',
                                makeEmptyDirs: false
                            ]
                        ]
                    ]
                )
            }
        }
    }
}


