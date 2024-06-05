pipeline {
  agent any
  environment {
    branch = sh(returnStdout: true, script: 'git branch --show-current').trim()
  }

  stages {
   stage("Checkout beta"){
            when{
                branch 'dev'
            }
                 git branch: 'dev', credentialsId: 'ci-mekdep', url: 'https://github.com/NaZyM0101/test-fo-multi'
    
            
            steps{
             script{
               def appDir = Jenkins.instance.getItemByFullName("${env.JOB_NAME}")
            echo "you are now in dev branch"

            echo "Your appdir is ${appDir}"
        }}
        }
        stage("Checkout main"){
            when{
                branch 'main'
            }

            steps{
                git branch: 'main', credentialsId: 'ci-mekdep', url: 'https://github.com/NaZyM0101/test-fo-multi'
              script{  
              def appDir = Jenkins.instance.getItemByFullName("${env.JOB_NAME}")
                echo "you are now in main branch this is second tesst"
                echo "Your appdir is ${appDir}"
        }}
        }
    stage("Final") {
      steps {
        echo "hello"
      }
    }
  }
}
