#!groovy

pipeline {
  agent none

  options {
    ansiColor('xterm')
    timestamps()
  }

  stages {
    stage('Build and scan') {
      agent { label 'ecs-builder-node14' }
      steps {
        script {
          initBuild()
          sh 'yarn install'
          securityScan()
          sh 'yarn lint'
          sh 'yarn build'

          if (env.BRANCH_NAME == '7.13') {
            publishNewNpmVersionIfAny("./package.json", ".")
          }
        }
      }
    }
  }
}
