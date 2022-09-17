node
{
 
  stage("CheckOutCodeGit")
  {
   git branch: 'main', url: 'https://github.com/loky1997/AXYYA-DIGITAL-ASSESMENT-LB1.git'
 }
 
 stage("Build")
 {
 nodejs(nodeJSInstallationName: 'nodejs14') {
        sh 'npm install'
    }
  stage("Docker Build"){
  sh "docker build -t dockerlokeshhs/nodejs14 ."
 }
  stage("docker login and push"){
  withCredentials([string(credentialsId: 'DOKCER_HUB_PASSWORD', variable: 'DOKCER_HUB_PASSWORD')]) {
          sh "docker login -u dockerlokeshhs -p ${DOKCER_HUB_PASSWORD}"
  }
   sh "docker push dockerlokeshhs/nodejs14"
 }
  stage("Deploy To Kuberates Cluster"){
   
  sh "kubectl apply -f nodejs.yml"
   
 }
  
}
