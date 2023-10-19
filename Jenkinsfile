pipeline {
    agent any

    stages {
        stage('Checkout Code from GitHub') {
            steps {
                // Check out your Node.js project from GitHub
                checkout([$class: 'GitSCM', branches: [[name: '*/main']], doGenerateSubmoduleConfigurations: false, extensions: [], userRemoteConfigs: [[url: 'https://github.com/hacetheworld/ecommerce-store.git']]])
            }
        }

        stage('Scan with Gitleaks in Docker') {
            steps {
                script {
                    // Run Gitleaks in a Docker container and output JSON
                    sh 'docker run --rm -v $PWD:/code zricethezav/gitleaks --path=/code --config=/code/.gitleaks.toml --format=json > gitleaks-reports.json'
                }
            }
        }
    }

    post {
        success {
            // Actions to take on successful build
            // You can notify, deploy, or perform other actions here
        }
        failure {
            // Actions to take on build failure
            // You can send notifications or take corrective actions
        }
    }
}
