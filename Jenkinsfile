
pipeline {
   agent any


   stages {
       stage('Sonar Analysis') {
           steps {
               echo 'CODE QUALITY CHECK'
               sh 'cd webapp && sudo docker run  --rm -e SONAR_HOST_URL="http://65.0.85.111:9000" -e SONAR_LOGIN="sqp_42f36121d19d2d2a2ae185d01094541d7a5dec9d"  -v ".:/usr/src" sonarsource/sonar-scanner-cli -Dsonar.projectKey=lms'
               echo 'CODE QUALITY DONE'
           }
       }
       stage('Build LMS') {
           steps {
               echo 'BUILD LMS APP'
               sh 'cd webapp && npm install && npm run build'
               echo 'BUILD COMPLETED'
           }
       }
       stage('Release LMS') {
           steps {
 script {
                   echo "RELEASE LMS Artifacts"      
                   def packageJSON = readJSON file: 'webapp/package.json'
                   def packageJSONVersion = packageJSON.version
                   sh "zip webapp/lms-${packageJSONVersion}.zip -r webapp/dist"
                   sh "curl -v -u admin:Avdhut@8140 --upload-file webapp/lms-${packageJSONVersion}.zip http://65.0.85.111:8081/repository/LMS/"    
                   sh "sudo rm -rf dist"
           }
           }
       }


       stage('Deploy LMS') {
           steps {
               script {
                   echo "Deploy LMS"      
                   def packageJSON = readJSON file: 'webapp/package.json'
                   def packageJSONVersion = packageJSON.version
                   sh "curl -u admin:lms12345 -X GET \'http://65.0.85.111:8081/repository/LMS/lms-${packageJSONVersion}.zip\' --output lms-'${packageJSONVersion}'.zip"
                   sh 'sudo rm -rf /var/www/html/*'
                   sh "sudo unzip -o lms-'${packageJSONVersion}'.zip"
                   sh "sudo cp -rf webapp/dist/* /var/www/html"           
                   sh "sudo rm -rf dist"
           }
           }
       }

        stage('Deploy LMS') {
           steps {
               script {
                   sleep(10)
                   echo "Deploy LMS"      
                   def packageJSON = readJSON file: 'webapp/package.json'
                   def packageJSONVersion = packageJSON.version
                   sh "curl -u admin:lms12345 -X GET \'http://65.0.85.111:8081/repository/LMS/lms-${packageJSONVersion}.zip\' --output lms-'${packageJSONVersion}'.zip"
                   sh 'sudo rm -rf /var/www/html/*'
                   sh "sudo unzip -o lms-'${packageJSONVersion}'.zip"
                   sh "sudo cp -r webapp/dist/* /var/www/html"           
           }
           }
       }


   }
}
