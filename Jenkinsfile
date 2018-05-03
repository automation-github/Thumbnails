pipeline {
  agent any
  stages {
    stage('thumbnails_rb') {
      steps {
        build 'test_thumbnails_rb_5.1'
      }
    }
    stage('thumbnails_vod') {
      steps {
        build 'test_thumbnails_vod_5.1'
      }
    }
    stage('copy xmls') {
      steps {
        sh 'scp -p root@$target_cluster:/tmp/Thumbnails/*.xml .'
      }
    }
    stage('error') {
      steps {
        junit(testResults: '*.xml', healthScaleFactor: 1, allowEmptyResults: true)
      }
    }
  }
  environment {
    target_cluster = '10.65.173.162'
  }
}