node{
    def mavenhome = tool name: "maven3.9.0"
    echo "the job name is : ${env.JOB_NAME}"
    echo "the Branch name is : ${env.BRANCH_NAME}"
    echo "the node name is : ${env.NODE_NAME}"
    stage ('Checkoutcode'){
   git branch: 'development', credentialsId: 'b037acf6-2509-403d-b519-ac7c67f7c92c', url: 'https://github.com/manju551609/maven-web-application.git'
    }
    stage('Build'){
        sh "${mavenhome}/bin/mvn clean package"
    }
    stage ('ExecuteSonarqubeReport'){
        sh "${mavenhome}/bin/mvn sonar:sonar"
    }
    stage ('UploadArtifactsIntoNexus'){
        sh "${mavenhome}/bin/mvn deploy"
    }
    stage ('DeployAppintoTomcatServer'){
        sshagent(['3cf4b959-bbb3-44aa-80fe-cfdcfa18d182']){
        sh "scp -o StrictHostKeyChecking=no target/maven-web-application.war ec2-user@172.31.26.243:/opt/apache-tomcat-9.0.71/webapps"
    }
}
}
