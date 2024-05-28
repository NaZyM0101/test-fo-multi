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
        //def branch = sh(returnStdout: true, script: 'git branch --show-current').trim()
        echo "Current branch: ${env.BRANCH_NAME}"
        SCB = "branch: ${env.BRANCH_NAME}"
        def lastSuccessBuildName = Jenkins.instance.getItemByFullName("${env.JOB_NAME}")?.lastSuccessfulBuild
        def lastSuccessBuildTime = Jenkins.instance.getItemByFullName("${env.JOB_NAME}")?.lastSuccessfulBuild.getTimestamp().format("yyyy-MM-dd HH:mm:ss")
        echo "Last Successful Build Name: ${lastSuccessBuildName}"
        LastSuccessName = "${lastSuccessBuildName.displayName}"
        LastSuccessTime = "${lastSuccessBuildTime}"
          echo "Test for branch ${env.BRANCH_NAME}"
      }
      // Use a dedicated library for notifications (recommended)
      // Assuming a library named 'mattermostNotifier' is installed
      mattermostSend(
        // Replace with your channel name
        message: " App build: '${env.JOB_NAME}' ${SCB} \n Status: **Success** [#${env.BUILD_NUMBER}](${env.BUILD_URL}/console)\n Last Successful Build id: [${LastSuccessName}](https://ci.mekdep.org/job/Multi_test/job/${env.BRANCH_NAME}/) time: [${LastSuccessTime}](https://ci.mekdep.org/job/Multi_test/job/${env.BRANCH_NAME}/lastSuccessfulBuild/)\n ChangeLog: [Link](https://ci.mekdep.org/job/Multi_test/job/${env.BRANCH_NAME})\n"
       )
    }
     failure{
        script{
         //def branch = sh(returnStdout: true, script: 'git branch --show-current').trim()
        echo "Current branch: {env.BUILD_NUMBER}"
        SCB = "branch: {env.BUILD_NUMBER}"
        def lastSuccessBuildName = Jenkins.instance.getItemByFullName("${env.JOB_NAME}")?.lastSuccessfulBuild
        def lastSuccessBuildTime = Jenkins.instance.getItemByFullName("${env.JOB_NAME}")?.lastSuccessfulBuild.getTimestamp().format("yyyy-MM-dd HH:mm:ss")
        echo "Last Successful Build Name: ${lastSuccessBuildName}"
      }
      // Use a dedicated library for notifications (recommended)
      mattermostSend(
        color: "#FF0000",
    message: " App build: '${env.JOB_NAME}' ${SCB} \n Status: **Failed** [#${env.BUILD_NUMBER}](${env.BUILD_URL}/console)\n Last Successful Build id: [${LastSuccessName}](https://ci.mekdep.org/job/Multi_test/job/${env.BRANCH_NAME}/) time: [${LastSuccessTime}](https://ci.mekdep.org/job/Multi_test/job/${env.BRANCH_NAME}/lastSuccessfulBuild/)\n ChangeLog: [Link](https://ci.mekdep.org/job/Multi_test/job/${env.BRANCH_NAME})\n"
       )
    }        
      
    }
  }

