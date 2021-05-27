
node{
   def buildNumber = BUILD_NUMBER 
    stage("git clone"){
        git url: "https://github.com/visureddy247/maven-web-application.git", branch: "master"
    }
    stage("maven clean package"){
     def mavenHome= tool name: "maven-3.6.3", type: "maven"
     sh "${mavenHome}/bin/mvn clean package"
}
    stage("build docker image"){
        sh "docker build -t visureddy247/maven-web-app:${buildNumber} ."
    }
    stage("docker login nd push"){
      withCredentials([string(credentialsId: 'Docker', variable: 'Docker')]) {
   sh "docker login -u visureddy247 -p ${Docker}"
    }
  sh "docker push visureddy247/maven-web-app:${buildNumber}"
           }
    stage("Deploy to Kubernetes"){
        sh " kubectl apply -f mavenwebappRS.yml"
    }   
}
