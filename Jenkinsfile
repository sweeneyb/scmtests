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
        script {
          echo "${env.BRANCH_NAME} is the branch_name"
          if (BRANCH.contains('multi')) {
            echo 'I am in the multi conditional'
            echo "branch is ${BRANCH}"
          } else {
              echo "branch is ${BRANCH}"
          }
          def values = "${BRANCH}".split("/")
          echo ""+values.size()

          echo "type: ${type}"
          echo "name: ${name}"
          def name = ""
          if (values.size() == 1) {
            name = "${values[1]}"
            echo "this would be a develop branch with branch tag ${name}"
            name = "${values[0]}"
          } else {
            def type = "${values[0]}"
            name = "${values[1]}"
            echo "this would be a ${type} branch with branch tag ${name}"

          }
        }
      }
    }
  } 
}