pipeline {
  agent any

  environment {
    COMMIT_HASH = sh(returnStdout: true, script: 'git rev-parse --short=4 HEAD').trim()
    BRANCH = "${env.GIT_BRANCH}"
    TAG_SUFFIX = ".${env.COMMIT_HASH}.${env.BUILD_NUMBER}"
    VERSION = "${env.TAG}"
  }

  enum BRANCH_TYPE {
    DEVELOP,
    FEATURE
  }

  def getSourceBranchType(String name) {
    if(name.split("/") == 1) {
      return BRANCH_TYPE.DEVELOP
    } else {
      return BRANCH_TYPE.FEATURE
    }
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
          def name = ""
          def TAG = ""
          echo ""+getSourceBranchType(BRANCH)
          if (values.size() == 1) {
            name = "${values[0]}"
            echo "this would be a develop branch with branch tag ${name}"
            TAG = "develop"+TAG_SUFFIX
          } else {
            def type = "${values[0]}"
            name = "${values[1]}"
            echo "this would be a ${type} branch with branch tag ${name}"
            TAG = "${name}"+TAG_SUFFIX
          }
          echo "${TAG}"
        }
      }
    }
  } 
}