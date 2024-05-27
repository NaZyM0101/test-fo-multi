pipeline{
    agent any

    stages{
        stage("Checkout beta"){
            when{
                branch 'dev'
            }
            steps{
            git branch: 'dev', credentialsId: 'ci-mekdep', url: 'https://github.com/NaZyM0101/test-fo-multi'
            echo "you are now in dev branch"
        }
        }
        stage("Checkout main"){
            when{
                branch 'main'
            }
            steps{
                git branch: 'main', credentialsId: 'ci-mekdep', url: 'https://github.com/NaZyM0101/test-fo-multi'
                echo "you are now in main branch"
        }
        }
    }
  post {
    success {
      script {
        def branch = sh(returnStdout: true, script: 'git branch --show-current').trim()
        echo "Current branch: ${branch}"
        SCB = "branch: ${branch}"
        def lastSuccessBuildName = Jenkins.instance.getItemByFullName("Multi_test/${branch}")?.lastSuccessfulBuild
          echo "Now its test ${env.JOB_NAME}"
          echo "Last Success ${lastSuccessBuildName}"
      }
      // Use a dedicated library for notifications (recommended)
      // Assuming a library named 'mattermostNotifier' is installed


    failure {
      script {
        def branch = sh(returnStdout: true, script: 'git branch --show-current').trim()
        echo "Current branch: ${branch}"
        SCB = "branch: ${branch}"
        def lastSuccessBuildName = Jenkins.instance.getItemByFullName("Multi_test/${branch}")?.lastSuccessfulBuild
        echo "Now its test ${env.JOB_NAME}"
        echo "Last Success ${lastSuccessBuildName}"
      }
      // Use a dedicated library for notifications (recommended)
      mattermostSend(
        color: "#FF0000",
        message: " App build: '${env.JOB_NAME}' ${SCB} \n Status: **Failed** [#${env.BUILD_NUMBER}](${env.BUILD_URL}/console)\n Last Successful Build id: [${lastSuccessBuildName}](https://ci.mekdep.org/job/Go-SMPP/lastSuccessfulBuild/) time: [${lastSuccessBuildName}](https://ci.mekdep.org/job/Go-SMPP/lastSuccessfulBuild/)\n ChangeLog: [Link](https://ci.mekdep.org/job/Go-SMPP/changes) \n"
      )
    }
  }
}
