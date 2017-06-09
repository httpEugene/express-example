pipeline {
  agent any
  stages {
    stage('Git') {
      steps {
        parallel(
          "Service1": {
            sh '''pwd
mkdir service1
cd service1'''
            git(url: 'https://github.com/httpEugene/express-example.git', branch: 'master')
            
          },
          "Service2": {
            sh '''pwd
mkdir service2
cd service2'''
            git(url: 'https://github.com/httpEugene/express-service.git', branch: 'master')
            
          }
        )
      }
    }
    stage('Build') {
      steps {
        parallel(
          "Service1": {
            sh '''pwd
npm install'''
            
          },
          "Service2": {
            sh '''pwd
npm install'''
            
          }
        )
      }
    }
    stage('Test') {
      steps {
        parallel(
          "Service1": {
            sh 'npm test-unit'
            
          },
          "Service2": {
            sh 'npm test-unit'
            
          }
        )
      }
    }
    stage('Cleanup') {
      steps {
        parallel(
          "Service1": {
            cleanWs(cleanWhenAborted: true, cleanWhenFailure: true, cleanWhenNotBuilt: true, cleanWhenSuccess: true, cleanWhenUnstable: true, cleanupMatrixParent: true, deleteDirs: true)
            
          },
          "Service2": {
            cleanWs(cleanWhenAborted: true, cleanWhenFailure: true, cleanWhenNotBuilt: true, cleanWhenSuccess: true, cleanWhenUnstable: true, cleanupMatrixParent: true, deleteDirs: true)
            
          }
        )
      }
    }
    stage('Compliting') {
      steps {
        echo 'Completed'
      }
    }
  }
}