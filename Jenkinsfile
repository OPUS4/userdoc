#!groovy

pipeline {
    agent any

    stages {
        stage('build') {
            steps{
                sh 'pwd'

                // install required bundles
                sh 'bundle install'

                // build documentation
                sh 'bundle exec jekyll build'
            }
        }
    }
}

