#!/usr/bin/env groovy

node {

  currentBuild.result = "SUCCESS"

    try {

      stage('Env') {
          sh 'node -v'
          sh 'npm -v'
          sh 'yarn --version'
      }

      stage('Pull code') {
        checkout scm
      }

      stage('Install dependencies') {
        nvm('version': 'v6.11.2') {
          sh 'node -v'
          sh 'npm -v'
          sh 'npm prune'
          sh 'npm install -g yarn@0'
          sh 'yarn'
        }
      }

      /*
      stage('Check syntax') {
        sh 'npm run lint'
      }

      stage('Run test') {
        env.NODE_ENV = "test"
        sh 'npm run test'
      }

      stage('Build with aot') {
        sh 'npm run build:aot'
      }

      */

      /*
      stage('Build Docker') {
        sh 'npm run build:docker'
      }

      stage('Deploy') {
        echo 'Push to Repo'
        sh './dockerPushToRepo.sh'
      }
       */

      stage('Cleanup') {
        echo 'prune and cleanup'
        sh 'npm prune'
        sh 'rm node_modules -rf'
      }
    }
    catch (err) {
      currentBuild.result = "FAILURE"
      throw err
    }
}
