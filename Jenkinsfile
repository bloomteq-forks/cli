#!/usr/bin/env groovy

jenkinsHelpersCredsId = 'github-deploy-key'

fileLoader.withGit('git@github.com:darktempla/jenkins-helpers.git', 'master', jenkinsHelpersCredsId, '') {
  utils = fileLoader.load('utils.groovy')
  builds = fileLoader.load('builds.groovy')
}

pipeline {
    options { buildDiscarder(logRotator(numToKeepStr: '5')) }
    agent {
        kubernetes {
            yamlFile 'jenkins.yaml'
            defaultContainer 'golang'
        }
    }
    stages {
        stage('Build Tekton CLI') {
          steps {
            script {
              sh 'make cross-popular'
              sh 'ls -alh ./bin'
            }
          }
        }
    }
}
