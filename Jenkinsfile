pipeline {
  agent any
  stages {
    stage('Git') {
      steps {
        sh '''pwd
git clone https://github.com/httpEugene/express-example.git
pwd
git clone https://github.com/httpEugene/express-service.git
pwd
git clone https://github.com/httpEugene/express-service3.git'''
      }
    }
    stage('Build') {
      steps {
        parallel(
          "Service1": {
            sh '''cd express-example
pwd
yarn --mutex /var/lib/jenkins/workspace/.yarn-mutex'''
            
          },
          "Service2": {
            sh '''cd express-service
pwd
yarn --mutex /var/lib/jenkins/workspace/.yarn-mutex'''
            
          },
          "Service3": {
            sh '''cd express-service3
pwd
yarn --mutex /var/lib/jenkins/workspace/.yarn-mutex'''
            
          }
        )
      }
    }
    stage('Package') {
      steps {
        parallel(
          "Service1": {
            sh '''cd express-example
npm run test-unit'''
            
          },
          "Service2": {
            sh '''cd express-service
npm run test-unit'''
            
          },
          "Service3": {
            sh '''cd express-service3
npm run test-unit'''
            
          }
        )
      }
    }
    stage('Deploy') {
      steps {
        parallel(
          "Service1": {
            sh '''cd express-example
npm run test-unit'''
            
          },
          "Service2": {
            sh '''cd express-service
npm run test-unit'''
            
          },
          "Service3": {
            sh '''cd express-service3
npm run test-unit'''
            
          }
        )
      }
    }
    stage('Test') {
      steps {
        parallel(
          "Test:S1": {
            sh '''cd express-example
npm run test-unit'''
            
          },
          "QualityCheck:S1": {
            sh 'echo \'working on quality S1\''
            
          },
          "Test:S2": {
            sh '''cd express-service
npm run test-unit'''
            
          },
          "QualityCheck:S2": {
            sh 'echo \'working on quality S2\''
            
          },
          "Test:S3": {
            sh '''cd express-service3
npm run test-unit'''
            
          },
          "QualityCheck:S3": {
            sh 'echo \'working on quality S3\''
            
          }
        )
      }
    }
    stage('Integration Tests') {
      steps {
        sh '''cd express-example
npm run test-integration'''
      }
    }
    stage('Cleanup') {
      steps {
        cleanWs(cleanWhenAborted: true, cleanWhenNotBuilt: true, cleanWhenFailure: true, cleanWhenSuccess: true, cleanWhenUnstable: true, cleanupMatrixParent: true, deleteDirs: true)
      }
    }
  }
}