pipeline {
    agent any
    
    environment {
        SCANNER_HOME = tool 'sonar-scanner'
    }

    stages {
        stage('Git Checkout') {
            steps {
                git branch: 'main', url: 'https://github.com/vaibhavchudari/10-MicroService-Appliction.git'
            }
        }
    stage('Sonarqube ') {
            steps {
                withSonarQubeEnv('sonar') {
                    sh ''' $SCANNER_HOME/bin/sonar-scanner -Dsonar.projectName=10-tier -Dsonar.projectKey=10-tier -Dsonar.java.binaries=. '''
                }
            }
        }
    stage('k8s-deploy') {
            steps {
                withKubeConfig(caCertificate: '', clusterName: 'my-eks8', contextName: '', credentialsId: 'k8-token', namespace: 'webapps', restrictKubeConfigAccess: false, serverUrl: 'https://7B304F48F795EA8E5092326F0742F18D.gr7.ap-south-1.eks.amazonaws.com') {
                        sh 'kubectl apply -f ./release/kubernetes-manifests.yaml'
                        sh 'kubectl get pods'
                        sh 'kubectl get svc'
                }
            }

        }
    }
}
