/* groovylint-disable LineLength */
pipeline {
  agent any

  tools { nodejs 'node' }

  stages {
    stage('Build') {
      steps {
        sh 'npm install'
      }
    }
    
    stage('test'){
       steps {
        sh 'node test'
      }
    }
  }
  post {
    failure {
      echo 'Processing failed'
    }
    success {
      step([$class: 'AWSEBDeploymentBuilder', credentialId: 'keven-lazio', zeroDowntime: false, skipEnvironmentUpdates: true,
      awsRegion:'us-east-1', applicationName: 'Sample', environmentName: 'Sample-env',
      bucketName: 'elasticbeanstalk-us-east-1-356337751874', rootObject: '.', includes: '**/*', excludes: '', versionLabelFormat: "main-${BUILD_NUMBER}", versionDescriptionFormat: "main-${BUILD_NUMBER}-env"])
    }
  }
}
