#!/usr/bin/env groovy

stage ('Checkout'){
	node {
		checkout scm
	}
}

stage ('Build') {
	node {
		echo "My branch is: ${env.BRANCH_NAME}"
		bat 'gradlew --refresh-dependencies clean assemble'
	}
}