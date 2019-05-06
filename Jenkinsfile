node('linux') {
    stage('Unit Tests') {
      git 'https://github.com/safa1611/java-project.git'
      sh 'ant -f test.xml -v'
      junit 'reports/result.xml'
    }
    stage('Build') {
      sh 'ant -f build.xml -v'
    }
    stage('Deploy'){
        sh 'aws s3 cp /workspace/java-pipeline/dist/rectangle-${BUILD_NUMBER}.jar s3://safa1611-assignment-4'
    }
    stage('Report'){
        
        withCredentials([[$class: 'AmazonWebServicesCredentialsBinding', accessKeyVariable: 'AWS_ACCESS_KEY_ID', credentialsId: '2b825de2-2fd1-416d-8d08-0e00f3ce1e53', secretKeyVariable: 'AWS_SECRET_ACCESS_KEY']]) {
        sh 'aws cloudformation describe-stack-resources --stack-name jenkins --region us-east-1' 
       }
    }
}
