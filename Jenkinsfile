pipeline {
   agent { label 'workstation' }


   stages {

     stage('code quality'){
       when {
         allOf {
           expression { env.TAG_NAME != env.GIT_BRANCH }
         }
       }
       steps {
         //sh 'sonar-scanner -Dsonar.host.url=http://172.31.42.81:9000 -Dsonar.login=admin -Dsonar.password=admin123 -Dsonar.projectKey=backend -Dsonar.qualitygate.wait=true'
         echo 'OK'
       }
     }

     stage('Unit Tests'){
       when {
         allOf {
           expression { env.TAG_NAME != env.GIT_BRANCH }
           branch 'main'
         }
       }
       steps {
         echo 'CI'
       }
     }

     stage('Release'){
        when {
          expression { env.TAG_NAME ==~ ".*" }
        }
//       steps {
//         sh 'zip -r frontend-${TAG_NAME}.zip static asset-manifest.json index.html robots.txt'
//         sh 'curl -sSf -u "admin:Admin123" -X PUT -T frontend-${TAG_NAME}.zip "http://artifactory.ayeeshadevops75.online:8081/artifactory/frontend/frontend-${TAG_NAME}.zip"'
//       }
        steps {
          sh 'docker build -t frontend 299627189740.dkr.ecr.us-east-1.amazonaws.com/frontend:${TAG_NAME} .'
          sh 'aws ecr get-login-password --region us-east-1 | docker login --username AWS --password-stdin 299627189740.dkr.ecr.us-east-1.amazonaws.com'
          sh 'docker push 299627189740.dkr.ecr.us-east-1.amazonaws.com/frontend:${TAG_NAME}'
        }

     }

   }
}
///