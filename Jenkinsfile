pipeline {
  agent any
  stages {
    stage('installation') {
      steps {
            sh 'python2.7 /var/tmp/Nightswatch/deploy/upgrade_machines_sa.py -p $target_cluster --ininame \'/var/lib/jenkins/nightswatch/5.1/config.ini\''
          }
    }
    stage('thumbnails_vod_5.1') {
      agent any
      environment {
        test_name = 'test_content_type_vod.py'
      }
      steps {
        build(job: 'test_thumbnails_vod_5.1', propagate: false)
      }
    }
    stage('thumnails_npvr_5.1') {
      agent any
      environment {
        test_name = 'test_content_type_npvr.py'
      }
      steps {
        build(job: 'test_thumnails_npvr_5.1', propagate: false)
      }
    }
    stage('thumbnails_negative_scenario_5.1') {
      agent any
      environment {
        test_name = 'test_content_type_negative_scenario.py'
      }
      steps {
        build(job: 'test_thumbnails_negative_scenario_5.1', propagate: false)
      }
    }
    stage('thumbnails_rb_5.1') {
      agent any
      environment {
        test_name = 'test_content_type_rb.py'
      }
      steps {
        build(job: 'test_thumbnails_rb_5.1', propagate: false)
      }
    }
    stage('copy xmls') {
      steps {
        sh '''scp -p root@$target_cluster:/tmp/Thumbnails/*.xml . '''
      }
    }
    stage('check_cores') {
      steps {
        sh 'ssh root@$target_cluster "python2.7 /var/Nightswatch/deploy/find_cores.py"'
      }
    }
    stage('publish junit results') {
      steps {
        junit(testResults: '*.xml', healthScaleFactor: 1.0, allowEmptyResults: true)
      }
    }
  }
  environment {
    target_cluster = '10.65.173.162'
  }
}
