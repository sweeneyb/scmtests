pipeline {
  agent any

  environment {
    COMMIT_HASH = sh(returnStdout: true, script: 'git rev-parse --short=4 HEAD').trim()
    BRANCH = "${env.GIT_BRANCH}"
    TAG = "${env.BRANCH}.${env.COMMIT_HASH}.${env.BUILD_NUMBER}".drop(15)
    DEV_TAG = "${env.BRANCH}.${env.COMMIT_HASH}.${env.BUILD_NUMBER}".drop(7)
    VERSION = "${env.TAG}"
  }

  stages {
    stage("list environment variables") {
      steps {
        sh "printenv | sort"
        echo "${DEV_TAG}.latest"
        script {
          if (BRANCH.contains('multi')) {
            echo 'I am in the multi conditional'
            echo "branch is ${BRANCH}"
            script {
              $VERSION = "${env.DEV_TAG}"
            }
            // withEnv([VERSION = "${env.DEV_TAG}"]) { //remove (['VERSION = ${env.DEV_TAG}'])
            // echo "${env.VERSION}"
            // }

            echo "${env.VERSION}"
          } else {
              echo "branch is ${BRANCH}"
          }
          def values = "${BRANCH}".split("/")
          def type = "${values[0]}"
          def name = "${values[1]}"
          echo "type: ${type}"
          echo "name: ${name}"
        }
      }
    }
  }
  
}