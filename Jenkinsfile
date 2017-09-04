#!/usr/bin/env groovy

stage ('Checkout'){
	node {
		checkout scm
		sh 'git submodule update --init' 
	}
}

stage ('Build') {
	node {
		echo "My branch is: ${env.BRANCH_NAME}"
		def flavor = flavor(env.BRANCH_NAME)
		echo "Building flavor ${flavor}"
		//build your gradle flavor, passes the current build number as a parameter to gradle
		sh "./gradlew clean assemble${flavor}Debug -PBUILD_NUMBER=${env.BUILD_NUMBER}"
	}
}

stage ('Archive') {
	node {
		archiveArtifacts artifacts: 'app/build/outputs/apk/*.apk', fingerprint: true
	}
}

// Pulls the android flavor out of the branch name the branch is prepended with /QA_
@NonCPS
def flavor(branchName) {
  def matcher = (env.BRANCH_NAME =~ /QA_([a-z_]+)/)
  assert matcher.matches()
  matcher[0][1]
}