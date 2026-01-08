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
    stage('adservice') {
            steps {
                script {
                    withDockerRegistry(credentialsId: 'docker-cred', toolName: 'docker') {
                            dir('/var/lib/jenkins/workspace/test/src/adservice') {
                                sh 'docker build -t vaibhavchudari/adservice:latest .'
                                sh 'docker push vaibhavchudari/adservice:latest'
                                sh 'docker rmi vaibhavchudari/adservice:latest'
                        }
                    }
                }
            }
        }
    stage('cartservice') {
            steps {
                script {
                    withDockerRegistry(credentialsId: 'docker-cred', toolName: 'docker') {
                            dir('/var/lib/jenkins/workspace/test/src/cartservice/src/') {
                                sh 'docker build -t vaibhavchudari/cartservice:latest .'
                                sh 'docker push vaibhavchudari/cartservice:latest'
                                sh 'docker rmi vaibhavchudari/cartservice:latest'
                        }
                    }
                }
            }
        }
    stage('checkoutservice') {
            steps {
                script {
                    withDockerRegistry(credentialsId: 'docker-cred', toolName: 'docker') {
                            dir('/var/lib/jenkins/workspace/test/src/checkoutservice') {
                                sh 'docker build -t vaibhavchudari/checkoutservice:latest .'
                                sh 'docker push vaibhavchudari/checkoutservice:latest'
                                sh 'docker rmi vaibhavchudari/checkoutservice:latest'
                        }
                    }
                }
            }
        }
    stage('currencyservice') {
            steps {
                script {
                    withDockerRegistry(credentialsId: 'docker-cred', toolName: 'docker') {
                            dir('/var/lib/jenkins/workspace/test/src/currencyservice') {
                                sh 'docker build -t vaibhavchudari/currencyservice:latest .'
                                sh 'docker push vaibhavchudari/currencyservice:latest'
                                sh 'docker rmi vaibhavchudari/currencyservice:latest'
                        }
                    }
                }
            }
        }
    stage('emailservice') {
            steps {
                script {
                    withDockerRegistry(credentialsId: 'docker-cred', toolName: 'docker') {
                            dir('/var/lib/jenkins/workspace/test/src/emailservice') {
                                sh 'docker build -t vaibhavchudari/emailservice:latest .'
                                sh 'docker push vaibhavchudari/emailservice:latest'
                                sh 'docker rmi vaibhavchudari/emailservice:latest'
                        }
                    }
                }
            }
        }
    stage('frontend') {
            steps {
                script {
                    withDockerRegistry(credentialsId: 'docker-cred', toolName: 'docker') {
                            dir('/var/lib/jenkins/workspace/test/src/frontend') {
                                sh 'docker build -t vaibhavchudari/frontend:latest .'
                                sh 'docker push vaibhavchudari/frontend:latest'
                                sh 'docker rmi vaibhavchudari/frontend:latest'
                        }
                    }
                }
            }
        }
    stage('loadgenerator') {
            steps {
                script {
                    withDockerRegistry(credentialsId: 'docker-cred', toolName: 'docker') {
                            dir('/var/lib/jenkins/workspace/test/src/loadgenerator') {
                                sh 'docker build -t vaibhavchudari/loadgenerator:latest .'
                                sh 'docker push vaibhavchudari/loadgenerator:latest'
                                sh 'docker rmi vaibhavchudari/loadgenerator:latest'
                        }
                    }
                }
            }
        }
    stage('paymentservice') {
            steps {
                script {
                    withDockerRegistry(credentialsId: 'docker-cred', toolName: 'docker') {
                            dir('/var/lib/jenkins/workspace/test/src/paymentservice') {
                                sh 'docker build -t vaibhavchudari/paymentservice:latest .'
                                sh 'docker push vaibhavchudari/paymentservice:latest'
                                sh 'docker rmi vaibhavchudari/paymentservice:latest'
                        }
                    }
                }
            }
        }
    stage('productcatalogservice') {
            steps {
                script {
                    withDockerRegistry(credentialsId: 'docker-cred', toolName: 'docker') {
                            dir('/var/lib/jenkins/workspace/test/src/productcatalogservice') {
                                sh 'docker build -t vaibhavchudari/productcatalogservice:latest .'
                                sh 'docker push vaibhavchudari/productcatalogservice:latest'
                                sh 'docker rmi vaibhavchudari/productcatalogservice:latest'
                        }
                    }
                }
            }
        }
    stage('recommendationservice') {
            steps {
                script {
                    withDockerRegistry(credentialsId: 'docker-cred', toolName: 'docker') {
                            dir('/var/lib/jenkins/workspace/test/src/recommendationservice') {
                                sh 'docker build -t vaibhavchudari/recommendationservice:latest .'
                                sh 'docker push vaibhavchudari/recommendationservice:latest'
                                sh 'docker rmi vaibhavchudari/recommendationservice:latest'
                        }
                    }
                }
            }
        }
    stage('shippingservice') {
            steps {
                script {
                    withDockerRegistry(credentialsId: 'docker-cred', toolName: 'docker') {
                            dir('/var/lib/jenkins/workspace/test/src/shippingservice') {
                                sh 'docker build -t vaibhavchudari/shippingservice:latest .'
                                sh 'docker push vaibhavchudari/shippingservice:latest'
                                sh 'docker rmi vaibhavchudari/shippingservice:latest'
                        }
                    }
                }
            }
        }
    stage('k8s-deploy') {
            steps {
                withKubeConfig(caCertificate: '', clusterName: 'my-eks8', contextName: '', credentialsId: 'k8-token', namespace: 'webapps', restrictKubeConfigAccess: false, serverUrl: 'https://7B304F48F795EA8E5092326F0742F18D.gr7.ap-south-1.eks.amazonaws.com') {
                        sh 'kubectl apply -f deployment-svc.yml'
                        sh 'kubectl get pods'
                        sh 'kubectl get svc'
                }
            }

        }
    }
}
