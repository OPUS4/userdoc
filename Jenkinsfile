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
                sh 'bundle exec jekyll build'
            }
        }

        stage('publish') {
            steps {
                archiveArtifacts artifacts: '_site/**'

                publishHTML(target: [
                    allowMissing: false,
                    alwaysLinkToLastBuild: false,
                    keepAll: true,
                    reportDir: 'userdoc',
                    reportFiles: '_site/**',
                    reportName: 'OPUS 4 Handbuch'
                ])
            }
        }
    }
}

