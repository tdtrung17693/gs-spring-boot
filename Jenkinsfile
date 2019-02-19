node {
   stage('init') {
      checkout scm
   }
   stage('build') {
      sh '''
         mvn clean package -f ./complete/pom.xml
         mkdir -p target
         cd complete/target
         cp ../src/main/resources/web.config web.config
         cp gs-spring-boot-0.1.0.jar app.jar 
         zip gs-spring-boot-0.1.0.zip app.jar web.config
      '''
   }
   stage('deploy') {
      azureWebAppPublish azureCredentialsId: env.AZURE_CRED_ID,
      resourceGroup: env.RES_GROUP, appName: env.WEB_APP, filePath: "**/gs-spring-boot-0.1.0.zip"
   }
}
