pipeline {
    agent any

    stages {
        stage('Install Bruno CLI') {
            steps {
                bat 'npm install -g @usebruno/cli'
            }
        }

        stage('Run Bruno Tests') {
            steps {
                bat '''
                bru run --env-file ./collections/collection1/environments/preprod.yml ^
                --reporter-json results.json ^
                --reporter-junit results.xml ^
                --reporter-html results.html
                '''
            }
        }

        stage('Publish Results') {
            steps {
                junit 'results.xml'
                archiveArtifacts artifacts: 'results.json, results.html', allowEmptyArchive: true
            }
        }
    }
}