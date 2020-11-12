pipeline {
  agent none
  stages {
    stage('build') {
      agent {
        docker {
          image 'lagairogo/carts-maven'
        }

      }
      steps {
        echo 'this is the build job'
        sh 'mvn compile'
      }
    }

    stage('test') {
      agent {
        docker {
          image 'lagairogo/carts-maven'
        }

      }
      steps {
        echo 'this is the test job'
        sh 'mvn test'
      }
    }

    stage('package') {
      agent {
        docker {
          image 'lagairogo/carts-maven'
        }

      }
      steps {
        echo 'this is the package job'
        sh 'mvn package'
      }
    }

    stage('Archive') {
      agent {
        docker {
          image 'lagairogo/carts-maven'
        }

      }
      steps {
        archiveArtifacts '**/target/*.jar'
      }
    }

    stage('Build&Publish') {
      steps {
        script {
          docker.withRegistry('https://index.docker.io/v1/', 'dockerlogin') {
            def dockerImage = docker.build("ferozedockerhub/shopping-carts:v${env.BUILD_ID}", "./")
            dockerImage.push()
            dockerImage.push("latest")
          }
        }

      }
    }

  }
  tools {
    maven 'Maven 3.6.3'
  }
  post {
    always {
      echo 'this pipeline has completed...'
    }

  }
}