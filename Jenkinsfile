pipeline {
    agent any
    options {
        skipStagesAfterUnstable()
    }
    stages {
        stage('Test') {
            steps {
		sh 'ls -al'
		sh 'pwd'
                echo 'main test ci/cd'
            }
        }
    }
}
