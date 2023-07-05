pipeline {
   agent any
   options {
      skipStagesAfterUnstable()
   }
   stages {
      stage('Test') {
         steps {
            /*
                    Для отправки проекта на сервер используется rsync, для авторизации используется SSH private key,
                      который был добавлен в Credentianls Jenkin'sa (credentialsId).
            */
            withCredentials([sshUserPrivateKey(credentialsId: 'ssh-greenbabyborn-green', keyFileVariable: 'keyfile')]) {
               sh 'rsync -e "ssh -i ${keyfile} -o StrictHostKeyChecking=no" -avz . "green@greenbabyborn.ru:~/test-cicd"'
            }
            sshagent(['ssh-greenbabyborn-green']) {
               sh 'ssh -o StrictHostKeyChecking=no green@greenbabyborn.ru uptime'
               sh 'ls -al'
               sh 'pwd'
            }
            echo 'main test ci/cd'
         }
      }
   }
}
