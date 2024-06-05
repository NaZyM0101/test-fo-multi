pipeline {
  agent any
  environment {
    branch = sh(returnStdout: true, script: 'git branch --show-current').trim()
  }

  stages {
    stage("Checkout Branch") {
      when {
        expression { branch =~ /(dev|main)/ } // Check for either 'dev' or 'main' branch
      }
      steps {
        git branch: "${env.branch}", credentialsId: 'ci-mekdep', url: 'https://github.com/NaZyM0101/test-fo-multi'
        script {
          echo "Switched to branch: ${env.branch}"
          def appDir = Jenkins.instance.getItemByFullName("${env.JOB_NAME}")
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
