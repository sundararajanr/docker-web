node{
     
    def buildnumber=BUILD_NUMBER ;
    stage('Git Checkout'){
        git url: 'https://github.com/sundararajanr/docker-web.git',branch: 'master'
    }
    
     stage(" MavenPackage"){
      def mavenHome =  tool name: "maven_3.6.3", type: "maven"
      def mavenCMD = "${mavenHome}/bin/mvn"
      sh "${mavenCMD} clean package"
    } 
    
    stage('Build Docker Image'){
        sh "docker build -t rsundararajandocker/java-web-app:${buildnumber} ."
    }
    
    stage('Push Docker Image'){
        withCredentials([string(credentialsId: 'DOCKER_HUB_CRED', variable: 'DOCKER_HUB_CRED')]) {
          sh "docker login -u rsundararajandocker -p ${DOCKER_HUB_CRED}"
        }
        sh "docker push rsundararajandocker/java-web-app:${buildnumber}"
     }
    
    
}
