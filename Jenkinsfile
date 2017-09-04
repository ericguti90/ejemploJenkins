#!/usr/bin/env groovy

stage ('Checkout'){
	node {
		checkout scm
	}
}

stage ('Build') {
	node {
		echo "My branch is: ${env.BRANCH_NAME}"
		//build your gradle flavor, passes the current build number as a parameter to gradle
		checkout scm
		sh "./gradlew clean assembleDebug"
	}
}