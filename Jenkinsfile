pipeline {
  agent any
  environment {
    branch = sh(returnStdout: true, script: 'git branch --show-current').trim()
  }

  stages {
    stage("Checkout beta") {
      when {
        branch 'dev'
      }
      steps {
        git branch: 'dev', credentialsId: 'ci-mekdep', url: 'https://github.com/NaZyM0101/test-fo-multi'
        script {
          echo "you are now in dev branch"
          def appDir = Jenkins.instance.getItemByFullName("${env.JOB_NAME}").getName()
          echo "Your appdir is ${appDir}"
        }
      }
    }
    stage("Checkout main") {
      when {
        branch 'main'
      }
      steps {
        git branch: 'main', credentialsId: 'ci-mekdep', url: 'https://github.com/NaZyM0101/test-fo-multi'
        script {
          echo "you are now in main branch this is second tesst"
          def appDir = Jenkins.instance.getItemByFullName("${env.JOB_NAME}").getName()
          
          echo "Your appdir is ${appDir}, ${env.JOB_NAME}"
        }
      }
    }
    stage("Final") {
      steps {
        echo "hello"
      }
    }
  }
}
