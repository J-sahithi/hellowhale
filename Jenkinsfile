pipeline {

  agent any

  stages {

    stage('Checkout Source') {
      steps {
        git url:'https://github.com/J-sahithi/hellowhale.git', branch: $branch
      }
    }
    
      stage("Build image") {
            steps {
                script {
                    myapp = docker.build("sahithij/hellowhale:${env.BUILD_ID}")
                }
            }
        }
    
      stage("Push image") {
            steps {
                script {
//                     docker.withRegistry('https://registry.hub.docker.com', 'dockerhub') {
                            myapp.push("latest")
                            myapp.push("${env.BUILD_ID}")
//                     }
                }
            }
        }

    
      stage('Deploy to Cluster') {
          steps {
            sh 'envsubst < ${WORKSPACE}/hellowhale.yml | kubectl apply -f -'
          }
      }

  }

}
