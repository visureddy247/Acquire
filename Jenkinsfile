
node{
   def buildNumber = BUILD_NUMBER 
    stage("git clone"){
        git url: "https://github.com/visureddy247/acquire.git", branch: "master"
    }
   
    stage("build docker image"){
        sh "docker build -t visureddy247/nginx-server-image:${buildNumber} ."
    }
    stage("docker login nd push"){
      withCredentials([string(credentialsId: 'Docker', variable: 'Docker')]) {
   sh "docker login -u visureddy247 -p ${Docker}"
    }
  sh "docker push visureddy247/nginx-server-image:VERSION:${buildNumber}"
           }
    stage("Deploy to Kubernetes"){
        sh " kubectl apply -f nginx.yml"
    }   
}
