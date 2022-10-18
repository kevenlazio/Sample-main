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
      step([$class: 'AWSEBDeploymentBuilder', credentialId: 'aws_mehroz', zeroDowntime: false, skipEnvironmentUpdates: true,
      awsRegion: 'ap-south-1', applicationName: 'Sample', environmentName: 'Sample-env',
      bucketName: 'elasticbeanstalk-ap-south-1-360464920616', rootObject: '.', includes: '**/*', excludes: '', versionLabelFormat: "main-${BUILD_NUMBER}", versionDescriptionFormat: "main-${BUILD_NUMBER}-env"])
    }
  }
}
