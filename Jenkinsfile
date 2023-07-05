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
		withCredentials([sshUserPrivateKey(credentialsId: "ssh-greenbabyborn-green", keyFileVariable: 'keyfile')]) {
       			stage('rsync') {
        			sh 'rsync -e "ssh -i ${keyfile} -o StrictHostKeyChecking=no" -avz . "green@greenbabyborn.ru:~/test-cicd"'
       			}
   		}
		
                echo 'main test ci/cd'
            }
        }
    }
}
