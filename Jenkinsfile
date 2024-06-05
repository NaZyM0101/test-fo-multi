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
          def branch = Jenkins.instance.getItemByFullName("${env.JOB_NAME}").getName()
          def appDir = "Multi_test_${branch}"
          echo "Your appdir is ${appDir}"
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
