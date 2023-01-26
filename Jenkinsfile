imagename = "044417216268.dkr.ecr.us-east-1.amazonaws.com/rentalcars"
ecrRegistry="https://044417216268.dkr.ecr.us-east-1.amazonaws.com"
awscreds = 'ecr:us-east-1:awsecrcreds'
node(){
stage("Git checkout"){
checkout scmGit(branches: [[name: '*/master']], extensions: [], userRemoteConfigs: [[credentialsId: 'gitcreds', url: 'https://github.com/muraliphani/rentalcarsv1.2.git']])
}

stage("Maven build"){
sh "mvn package"
}

stage("Build docker image"){
dockerImage = docker.build( imagename + ":$BUILD_NUMBER")

}

stage("Push docker image to ECR"){
                docker.withRegistry( ecrRegistry, awscreds) {
                dockerImage.push("$BUILD_NUMBER")
                dockerImage.push('latest')
              }
}

}