pipeline {

    agent {
        docker {
            image 'node:22'
            args '-u root'
        }
    }

    stages {
        stage('Install Bruno CLI') {
            steps {
                sh 'npm install -g @usebruno/cli'
            }
        }

        stage('Run Bruno Tests') {
            steps {
                sh '''
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