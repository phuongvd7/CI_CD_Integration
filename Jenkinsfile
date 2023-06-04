def mvnHome

node('node_slave'){
   stage('git checkout'){
      try {
       git branch: 'feature1', url: 'https://github.com/phuongvd7/CI_CD_Integration'
      } catch(err) {
         sh "echo error in checkout"
      }
   }
   
   stage('maven test'){
      try{
         mvnHome=tool 'Maven 3.6.3'
         sh "$mvnHome/bin/mvn --version"
         sh "$mvnHome/bin/mvn clean test surefire-report:report"
      } catch(err) {
         sh "echo error in defining maven"
      }
   }
   
   stage('test case and report'){
      try {
         echo "executing test cases"
         junit allowEmptyResults: true, testResults: '/home/ec2-user/workspace/ex1/workspace/test-pipleline-agent/addressbook_main/target/surefire-reports'
         publishHTML([allowMissing: false, alwaysLinkToLastBuild: false, keepAll: false, reportDir: '/home/ec2-user/workspace/ex1/workspace/test-pipleline-agent/addressbook_main/target/site', reportFiles: 'surefire-report.html', reportName: 'SureFireReportHTML', reportTitles: '', useWrapperFileDirectly: true])

      } catch(err){
         throw err
      }
   }

   // stage('package and generate artifacts'){
   //    try {
   //       sh "$mvnHome/bin/mvn clean package -DskipTests=true"
   //       archiveArtifacts allowEmptyArchive: true, artifacts: 'addressbook_main/target/**/*.war'
   //    } catch(err) {
   //       sh "echo error in packaging and generating artifacts"
   //    }
   // }

   // stage('deployment of application using docker'){
   //    try {
   //       sh "docker version"
   //       sh "docker build -t rbngtm1/archiveartifacts:newtag -f Dockerfile ."
   //       sh "docker run -p 8080:8080 -d rbngtm1/archiveartifacts:newtag"
   //       withDockerRegistry(credentialsId: 'docker-hub-registry') {
   //       sh "docker push rbngtm1/archiveartifacts:newtag"
   //       }
   //    } catch(err) {
   //       sh "echo error in deployment using docker"
   //    }
   // }

   // stage('deployment of an application'){
   //    try {
   //       sshagent(['target-key-shared']) {
   //          sh "scp -o StrictHostKeyChecking=no tomcat.sh ec2-user@10.0.0.137:/tmp"
   //          sh "scp -o StrictHostKeyChecking=no symlink_target.sh ec2-user@10.0.0.137:/tmp"
   //          sh "ssh -o StrictHostKeyChecking=no ec2-user@10.0.0.137 /tmp/tomcat.sh"
   //          sh "scp -o StrictHostKeyChecking=no addressbook_main/target/addressbook.war ec2-user@10.0.0.137:/tmp"
   //          sh "ssh -o StrictHostKeyChecking=no ec2-user@10.0.0.137 /tmp/symlink_target.sh"
   //       }
   //    } catch(err){
   //       echo "error in deployment of an application"
   //    }
   // }
   
   // stage('artifacts to s3'){
   //    try {
   //       withCredentials([[$class: 'AmazonWebServicesCredentialsBinding', accessKeyVariable: 'AWS_ACCESS_KEY_ID', credentialsId: 'deploytos3', secretKeyVariable: 'AWS_SECRET_ACCESS_KEY']]) {
   //          sh "aws s3 ls"
   //          sh "aws s3 mb s3://cloudyeti-bucket-for-aws"
   //          sh "aws s3 cp addressbook_main/target/addressbook.war s3://cloudyeti-bucket-for-aws"
   //       }
   //    } catch(err) {
   //       sh "echo error in sending artifacts to s3"
   //    }
   // }
}

