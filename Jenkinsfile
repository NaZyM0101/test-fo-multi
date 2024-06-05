pipeline{
    agent any
    environment{
        branch = sh(returnStdout: true, script: 'git branch --show-current').trim()
    }

    stages{
        stage("Checkout beta"){
            when{
                branch 'dev'
            }
            def appDir = Jenkins.instance.getItemByFullName("${env.JOB_NAME}")
            steps{
            git branch: 'dev', credentialsId: 'ci-mekdep', url: 'https://github.com/NaZyM0101/test-fo-multi'
            echo "you are now in dev branch"

            echo "Your appdir is ${appDir}"
        }
        }
        stage("Checkout main"){
            when{
                branch 'main'
            }
                            def appDir = Jenkins.instance.getItemByFullName("${env.JOB_NAME}")
            steps{
                git branch: 'main', credentialsId: 'ci-mekdep', url: 'https://github.com/NaZyM0101/test-fo-multi'
                
                echo "you are now in main branch this is second tesst"
                echo "Your appdir is ${appDir}"
        }
        }
        stage("Final"){
            steps{
                echo "hello"

            }
        }
    }

  }

