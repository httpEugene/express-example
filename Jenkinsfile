pipeline {
  agent any
  stages {
    stage('Git') {
      steps {
        parallel(
          "Service1": {
            sh '''pwd
git clone https://github.com/httpEugene/express-example.git
cd express-example
pwd

'''
            
          },
          "Service2": {
            sh '''pwd
git clone https://github.com/httpEugene/express-service.git
cd express-service
pwd'''
            
          }
        )
      }
    }
    stage('Build') {
      steps {
        parallel(
          "Service1": {
            sh '''cd express-example
pwd
npm install'''
            
          },
          "Service2": {
            sh '''cd express-service
pwd
npm install'''
            
          }
        )
      }
    }
    stage('Test') {
      steps {
        parallel(
          "Service1": {
            sh '''cd express-example
npm test-unit'''
            
          },
          "Service2": {
            sh '''cd express-service
npm test-unit'''
            
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