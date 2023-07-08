pipeline {
   agent any
   options {
      // Пропустит стадии выполенения pipeline, если появятся ошибки при выполнении
      skipStagesAfterUnstable()
   }
   stages {
      stage('Test') {
         steps {
            /*
                    Для отправки проекта на сервер используется rsync, для авторизации используется SSH private key,
                      который был добавлен в Credentianls Jenkin'sa (credentialsId).
            */
                //========================================================================================================================================================
                /*
            // Без использования плагинов Jenkins

                withCredentials([sshUserPrivateKey(credentialsId: 'ssh-greenbabyborn-green', keyFileVariable: 'keyfile')]) {
               sh 'rsync -e "ssh -i ${keyfile} -o StrictHostKeyChecking=no" -avz . "green@greenbabyborn.ru:~/test-cicd"'
               // Ниже можно писать команды, которые будут выполняться на сервере
               sh '''ssh -i ${keyfile} -o StrictHostKeyChecking=no green@greenbabyborn.ru << EOF
                       uptime
                       pwd
                       ls -al
               EOF'''
                }
                */

            //========================================================================================================================================================
            // С использованием плагина SSHAgent
            sshagent(['ssh-greenbabyborn-green']) {
               // Отпрвка проекта на сервер с помощью rsync, но private key передавать уже не нужно т.к.это делает плагин SSHAgent
               sh 'rsync -e "ssh -o StrictHostKeyChecking=no" -avz . "green@greenbabyborn.ru:~/test-cicd"'

               // Ниже можно писать команды, которые будут выполняться на сервере
               sh '''ssh -o StrictHostKeyChecking=no green@greenbabyborn.ru << EOF
                       uptime
                       pwd
                       ls -al
               EOF'''
            }
            echo 'main test ci/cd'
         }
      }
   }
}
