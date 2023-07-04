pipeline {
    agent any
    options {
        skipStagesAfterUnstable()
    }
    stages {
        stage('Test') {
            steps {
					 sh 'll'
					 sh 'pwd'
                echo 'main test ci/cd'
            }
        }
    }
}