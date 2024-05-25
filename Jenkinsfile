pipeline{
    agent any

    stages{
        stage("Checkout"){
            when{
                branch 'dev'
            }
            steps{
            git branch: 'dev', credentialsId: 'ci-mekdep', url: 'https://github.com/NaZyM0101/test-fo-multi'
            echo "you are now in dev branch"
        }
        }
        stage("Checkout"){
            when{
                branch 'main'
            }
            steps{
                git branch: 'main', credentialsId: 'ci-mekdep', url: 'https://github.com/NaZyM0101/test-fo-multi'
                echo "you are now in main branch"
        }
        }
    }
}
      post {
    success {
      script {
        def branch = sh(returnStdout: true, script: 'git branch --show-current').trim()
        echo "Current branch: ${branch}"
        SCB = "branch: ${branch}"
        def lastSuccessBuildTime = Jenkins.instance.getItem(env.JOB_NAME)
        echo "build ${lastSuccessBuildTime}"
    }

    failure {
      script {
        def branch = sh(returnStdout: true, script: 'git branch --show-current').trim()
        echo "Current branch: ${branch}"
        SCB = "branch: ${branch}"
        def lastSuccessBuildTime = Jenkins.instance.getItem(env.JOB_NAME)
        echo "build ${lastSuccessBuildTime}"
    }
  }
   }
   }
