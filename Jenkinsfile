pipeline {
  agent any
  stages {
    stage('Build') {
      steps {
        echo 'Build Demo Application'
        sh 'sh run_build_script.sh'
      }
    }

    stage('Linux Tests') {
      environment {
        Path = 'C:\\Users\\gabriel.job\\AppData\\Local\\Programs\\Git\\bin'
      }
      parallel {
        stage('Linux Tests') {
          steps {
            echo 'Run Linux tests'
            sh '''sh run_linux_tests.sh

'''
          }
        }

        stage('Windows Tests') {
          steps {
            echo 'Run Windows tests'
          }
        }

      }
    }

    stage('Deploy Staging') {
      steps {
        echo 'Deploy to staging environment'
        input 'Ok to deploy to production?'
      }
    }

    stage('Deploy Production') {
      steps {
        echo 'Deploy to Prod'
      }
    }

  }
  post {
    always {
      archiveArtifacts(artifacts: 'target/demoapp.jar', fingerprint: true)
    }

    failure {
      mail(to: 'gabe.e.job@gmail.com', subject: "Failed Pipeline ${currentBuild.fullDisplayName}", body: " For details about the failure, see ${env.BUILD_URL}")
    }

  }
}