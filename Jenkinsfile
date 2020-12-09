pipeline {

  agent any

  stages {

    stage('Checkout Source') {
      steps {
        git url:'https://github.com/NMDiaw97/flask-app-jenkins.git'
      }
    }
    
      stage("Build image") {
            steps {
                script {
                    myapp = docker.build("dockermaty1997/catnip:${env.BUILD_ID}")
                }
            }
        }
    
      stage("Push image") {
            steps {
                script {
                    docker.withRegistry('', 'dockermaty_id') {
                            myapp.push("latest")
                            myapp.push("${env.BUILD_ID}")
                    }
                }
            }
        }

    
    stage('Deploy App') {
      steps {
        script {
          kubernetesDeploy(configs: "catnip.yml", kubeconfigId: "kubediaf"
        }
      }
    }

  }

}
