imagename ="245654260615.dkr.ecr.us-east-1.amazonaws.com/rentalcars"
ecrRegistry ="https://245654260615.dkr.ecr.us-east-1.amazonaws.com"
awscreds = 'ecr:us-east-1:awsecrcreds'



node(){

   stage("Git Checkout"){
   checkout([$class: 'GitSCM', branches: [[name: '*/master']], extensions: [], userRemoteConfigs: [[credentialsId: 'repo3git', url: 'https://github.com/s9848261712/rentalcarsv1.2.git]]]}
                 }
        }

   stage("Maven Build"){
   sh "mvn package"
   }



  stage("Build Docker image"){

     dockerImage = docker.build( imagename + ":$BUILD_NUMBER")
  }


  stage('push docker image to ECR') {

          docker.withRegistry( ecrRegistry, awscreds) {
                dockerImage.push("$BUILD_NUMBER")
                dockerImage.push('latest')
              }
          }

}
