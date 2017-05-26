#!groovy

pipeline {
    agent any

    stages {
        stage('build') {
            steps {
                sh 'pwd'

                // install required bundles
                sh 'bundle install'

                // build documentation
                sh 'bundle exec jekyll build --config _config.yml,_config-ci.yml'
            }
        }

        stage('publish') {
            steps {
                archiveArtifacts artifacts: '_site/**'

                publishHTML(target: [
                    allowMissing: false,
                    alwaysLinkToLastBuild: false,
                    keepAll: true,
                    reportDir: '_site/',
                    reportFiles: 'index.html',
                    reportName: 'OPUS 4 Handbuch'
                ])
            }
        }
    }
}

