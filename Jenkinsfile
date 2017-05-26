#!groovy

pipeline {
    agent any

    stages {
        stage('prepare') {
            steps {
                writeFile([file: '_config-ci.yml', test: '/jenkins/job/OPUS%204%20User%20Documentation/job/4.6/OPUS_4_Handbuch'])
            }
        }

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

