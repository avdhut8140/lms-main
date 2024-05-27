
pipeline {
   agent any


   stages {
       stage('postgres') {
           steps {
                  sh 'git clone -b dev https://github.com/avdhut8140/lms-main.git'

               echo 'chake all yml file '
               sh 'cd postgress'

               echo 'build pg-secret.yml'
               sh "kubectl apply -f pg-secret.yml"

               echo 'build pg-deployment.yml'
               sh "kubectl apply -f pg-deployment.yml"

               echo 'build pg-service.yml'
               sh "kubectl apply -f pg-service.yml"

               echo 'build be-configmap.yml'
               sh "kubectl apply -f be-configmap.yml"
               echo 'CODE QUALITY DONE'
           }
       }
       stage('create and push image') {
           steps {
               sh 'cd lms/api'
               echo 'BUILD LMS image'
               sh 'docker build -t avdhut8140/lms-be .'

               echo 'push LMS image'
               sh 'docker push avdhut8140/lms-be:lms-1.1'
               echo 'COMPLETED pushing '
           }
       }
      
   }

}
