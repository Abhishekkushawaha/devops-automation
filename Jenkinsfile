pipeline {
    agent any
    tools{
        maven 'maven_3_9_6'
    }
    stages{
        stage('Build Maven'){
            steps{
                checkout([$class: 'GitSCM', branches: [[name: '*/main']], extensions: [], userRemoteConfigs: [[url: 'https://github.com/Abhishekkushawaha/devops-automation.git']]])
                sh 'mvn clean install'
            }
        }
        stage('Build docker image'){
            steps{
                script{
                    sh 'docker build -t abhikushali/devops-integration .'
                }
            }
        }
        stage('Push image to Hub'){
            steps{
                script{
                   //withCredentials([string(credentialsId: 'dockerhub-pwd', variable: 'dockerhubpwd')]) {
                   sh 'docker login -u abhikushali -p Welcometoisl@2024'

//}
                   sh 'docker push abhikushali/devops-integration'
                }
            }
        }
        stage('docker to k8s'){
            steps{
                script{
                  //sh 'ls /opt/homebrew/bin/ | grep oc'
                  //sh 'cd /opt/homebrew/bin'
                  //sh  'oc login --token=sha256~3upv90iLhBpXlEAJSHortQLddHysDSpcG0XHKImQosE --server=https://api.sec-patch.cp.fyre.ibm.com:6443'
                     //sh 'kubernetesDeploy (configs: "deploymentservice.yaml",kubeconfigId: "k8sconfigpwd")'
                // kubernetesApply createNewResources: true, deletePodsOnReplicationControllerUpdate: false, ignoreRunningOAuthClients: false, ignoreServices: false, processTemplatesLocally: false, readinessTimeout: 0, rollingUpgradePreserveScale: true, rollingUpgrades: true, servicesOnly: false
                 // sh 'kubectl --kubeconfig=/Users/abhishekkushawaha/.kube get ns development || kubectl --kubeconfig=/Users/abhishekkushawaha/.kube  create ns development")' && sh 'kubectl apply -f deploymentservice.yaml'
                // sh 'kubectl --kubeconfig=/Users/abhishekkushawaha/.kube apply -f deploymentservice.yaml'
                 //sh 'kubectl apply -f deploymentservice.yaml'
                 kubernetesDeploy (configs: 'deploymentservice.yaml', kubeconfigId: 'k8spassword')
                }
                  

            }
        }
    }
}