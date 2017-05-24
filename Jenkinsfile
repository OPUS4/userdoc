#!groovy

pipeline {
    agent any

    stages {
        stage('build') {
            steps{
                // install required bundles
                sh 'bundle install'

                // build documentation
                sh 'bundle exec jekyll build --config _config.yml,_localconfig.yml'
            }
        }
    }
}

