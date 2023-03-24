node {
    def WORKSPACE = "/var/lib/jenkins/workspace/springboot-demo-deploy"
    def dockerImageTag = "demo-deploy:latest"

try{
     stage('Clone Repo') {
        // for display purposes
        // Get some code from a GitHub repository
        git url: 'https://github.com/KaterinaN86/demo.git',
            credentialsId: 'my_credentials',
            branch: 'main'
     }
      stage('Build docker') {
             dockerImage = docker.build("demo-deploy:latest")
      }

      stage('Deploy docker'){
              echo "Docker Image Tag Name: ${dockerImageTag}"
              sh "docker stop demo-deploy || true && docker rm demo-deploy || true"
              sh "docker run --name demo-deploy -d -p 8082:8082 demo-deploy:latest"
      }
}catch(e){
    currentBuild.result = "FAILED"
    throw e
}
}