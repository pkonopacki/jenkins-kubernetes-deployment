pipeline {

  // environment {
  //   DOCKERHUB_CREDENTIALS = credentials('dockerhub-credentials')
  //   dockerImage = ""
  // }

  agent {
    node {
      label 'docker-agent-eclipse'
      args '-v $HOME/.m2:/root/.m2'
    }
  }

  stages {

    // stage('Checkout Source') {
    //   steps {
    //     git 'https://github.com/Bravinsimiyu/jenkins-kubernetes-deployment.git'
    //   }
    // }

    stage('Build image') {

      steps{
          sh 'docker build -t pkonopacki/react-app .' 
      }
    }

    stage('Login') {
      steps{
          sh 'echo $DOCKERHUB_CREDENTIALS_PSW | docker login -u $DOCKERHUB_CREDENTIALS_USR --password-stdin'  
      }
    }

    stage('Push') {
      steps{
        sh 'docker push pkonopacki/react-app:latest'

        //   docker.withRegistry( 'https://registry.hub.docker.com', registryCredential ) 
        //     dockerImage.push("latest")        
      }
    }

    // stage('Deploying React.js container to Kubernetes') {
    //   steps {
    //     script {
    //       kubernetesDeploy(configs: "deployment.yaml", "service.yaml")
    //     }
    //   }
    // }

  }

  post {
    always {
        sh 'docker logout'
    }
  }  

}