def isDevelopBranch(branchName) {
  return branchName.split("/").size() == 1
}

def getBranchInfo(branchName) {
  def branchInfo = [:]
  if(isDevelopBranch(branchName)) {
    branchInfo["type"] = "develop"
    branchInfo["name"] = branchName
    branchInfo["isDevelop"] = true
  } else {
    def details = branchName.split("/")
    branchInfo["type"] = details[0]
    branchInfo["name"] = details[1]
    branchInfo["isDevelop"] = false
  }
  return branchInfo
}

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
        //sh "printenv | sort"
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

          // if (values.size() == 1) {
          def branchInfo = getBranchInfo(BRANCH)
          if (branchInfo["isDevelop"]) {
            name = "${BRANCH}"
            echo "this would be a develop branch with branch tag ${name}"
            TAG = "develop"+TAG_SUFFIX
          } else {
            echo "this would be a ${branchInfo["type"]} branch with branch tag ${branchInfo["name"]}"
            TAG = "${branchInfo["name"]}"+TAG_SUFFIX
          }
          echo "Final tag is ${TAG}"
        }
      }
    }
  } 
}