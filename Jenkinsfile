pipeline {
    agent any

    stages {
        stage('Build') {
            steps {
               sh " docker container run -dt --name lms-db -e POSTGRES_PASSWORD=Avdhut@8140 postgres"
            }
        }


        stage('Test') {
            steps {
               stage('Start') {
  steps {
    script {
      def container = docker.image('mongo:latest').run('-p 27017:27017 --name mongodb -d')

      def ipAddress = null

      while (!ipAddress) {

        ipAddress = sh(
          returnStdout: true,
          script      : "docker inspect -f '{{range.NetworkSettings.Networks}}{{.IPAddress}}{{end}}' mongodb"
        )

        if (!ipAddress) {
          echo "Container IP address not yet available..."
          sh "sleep 2"
        }

      }

      echo "Got IP address = ${ipAddress}."
    }
  }
}
            }
        }



        
        stage('Deploy') {
            steps {
                echo 'Deploying....'
            }
        }
    }
}