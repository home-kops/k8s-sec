pipeline {
  agent {
    kubernetes {
      label 'agent-s'
    }
  }
  stages {
    stage('Clone') {
      steps {
        git branch: 'main',
          credentialsId: 'github-home-kops-token',
          url: 'https://github.com/home-kops/k8s-sec.git'
      }
    }

    stage('Verify') {
      steps {
        container('jnlp') {
          sh '''
            helm lint ./falco && \
              helm dependency build ./falco && \
              helm template ./falco -f ./falco/values.yaml
          '''

        }
      }
    }
  }
}
