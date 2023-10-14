pipeline {
   agent { label 'workstation' }

   stages {

     stage('code quality'){
       when {
         allOf {
           branch 'main'
           expression { env.TAG_NAME != env.BRANCH_NAME }
         }
       }
       steps {
         sh 'sonar-scanner -Dsonar.host.url=http://172.31.42.81:9000 -Dsonar.login=admin -Dsonar.password=admin123 -Dsonar.projectKey=frontend -Dsonar.qualitygate.wait=true'
       }
     }


     stage('Release'){
       when {
         expression { env.TAG_NAME ==~ ".*" }
       }
       steps {
         sh 'env'
         echo 'CI'
       }
     }
   }
}