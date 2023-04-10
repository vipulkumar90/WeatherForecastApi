pipeline {
    agent any

    stages {
        stage('checkout') {
            steps {
                checkout changelog: false, poll: false, scm: scmGit(branches: [[name: '*/master']], extensions: [], userRemoteConfigs: [[credentialsId: 'github', url: 'https://github.com/vipulkumar90/weatherForecastApi']])
            }
        }
        stage('build') {
            steps {
                dotnetBuild configuration: 'Debug', sdk: '.NET 6'
            }
        }
        stage('docker build') {
            steps {
                sh 'docker build -t weatherforecastapi:latest .'
            }
        }
        stage('docker run') {
            steps {
                sh 'docker run -p 5000:80 weatherforecastapi:latest'
            }
        }
    }
}
