pipeline {
  agent any

  environment {
    COMMIT_HASH = sh(returnStdout: true, script: 'git rev-parse --short=4 HEAD').trim()
    BRANCH = "${env.GIT_BRANCH}"
    TAG_SUFFIX = ".${env.COMMIT_HASH}.${env.BUILD_NUMBER}"
    VERSION = "${env.TAG}"
  }

  stages {
    stage("list environment variables") {
      steps {
        sh "printenv | sort"
        echo "${DEV_TAG}.latest"
        script {
          echo "${env.BRANCH_NAME} is the branch_name"
          if (BRANCH.contains('multi')) {
            echo 'I am in the multi conditional'
            echo "branch is ${BRANCH}"
            script {
              $VERSION = "${env.DEV_TAG}"
            }
          } else {
              echo "branch is ${BRANCH}"
          }
          def values = "${BRANCH}".split("/")
          echo values.size()
          def type = "${values[0]}"
          def name = "${values[1]}"
          echo "type: ${type}"
          echo "name: ${name}"
          if (values.size() == 1) {
            echo "this would be a develop branch with branch tag " +values[0]
          } else {
            echo "this would be a feature/hotfix branch with branch tag " +values[1]
          }
        }
      }
    }
  }
  
}