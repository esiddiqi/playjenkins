pipeline {

  agent { 
    kubernetes {
      defaultContainer 'mynginx'
      yaml '''
        apiVersion: v1
        kind: Pod
        spec:
          containers:
          - name: mynginx
            image: nginx
            command:
            - cat
            tty: true
        
      
      '''
    }
        
  }

  stages {

    stage('Checkout Source') {
      steps {
        git url:'https://github.com/esiddiqi/playjenkins.git', branch:'test-deploy-stage'
      }
    }

    stage('Deploy App') {
      steps {
        script {
          kubernetesDeploy(configs: "nginx.yaml", kubeconfigId: "mykubeconfig")
        }
      }
    }

  }

}
