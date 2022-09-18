pipeline{
    agent any

    environment {
        JAVA_VERSION="11"
        DEVOPS_BATCH=AUG2022
    }

    parameters {
      choice(name: 'DEPLOYMENT_ENV',
       choices: ['UAT1', 'UAT2', 'PREPOD'],
        description: 'SELECT THE ENV FOR DEPLOYMENT'
        )
        string(name: 'DUMMYSTR',
        description: 'Just a dummy value',
        defaultValue: 'Dharmendar')
    }

    trigger {
        pollSCM('* * * * * ')

    }
    options {
      buildDiscarder logRotator(artifactDaysToKeepStr: '', artifactNumToKeepStr: '', daysToKeepStr: '2', numToKeepStr: '2')
    }

    tools {
      jdk 'jdk11'
      maven 'jdk-demo'
    }

stages {
    stage('Checkout') {
        steps{
            checkout scm
        }
    }

        stage('Compile') {
            steps{
                sh 'mvn compile'
            }
    }

  }



post {
  always {
    slackSend channel: 'devops', message: 'this is the post message'
  }
}

}
