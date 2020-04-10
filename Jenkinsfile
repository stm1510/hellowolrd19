pipeline {
  agent any
  tools {
     maven 'M2_HOME'
  }
  stages {
     stage('build'){
        steps {
          echo "hello world"
          }
       }
    stage('test'){ 
        steps {
          echo "hello world"
          }
       }
    stage('deploy'){
        steps {
          echo "hello world"
          sh '''
          mvn clean
          mvn install
          mvn package
          mvn test
          mvn sonar:sonar \
  -Dsonar.projectKey=classproject \
  -Dsonar.host.url=http://192.168.1.178:9000 \
  -Dsonar.login=05f83f64542ad160c216a9a119d1c7e9bb99ec4c
     '''
          }
       }
    stage('deployment'){
        steps {
          retry(3) {
         deploy adapters: [tomcat8(credentialsId: 'TomcatID', path: '', url: 'http://3.91.226.58:8080/')], contextPath: null, war: '**/*war'
         sshPublisher(publishers: [sshPublisherDesc(configName: 'Docker-host', transfers: [sshTransfer(cleanRemote: false, excludes: '', execCommand: 'docker rmi pcontact:v.${BUILD_NUMBER}; docker build -t pcontact:v.${BUILD_NUMBER} .; docker tag pcontact:v.${BUILD_NUMBER} kserge2001/pcontact:v.${BUILD_NUMBER}; docker push kserge2001/pcontact:v.${BUILD_NUMBER};', execTimeout: 120000, flatten: false, makeEmptyDirs: false, noDefaultExcludes: false, patternSeparator: '[, ]+', remoteDirectory: '', remoteDirectorySDF: false, removePrefix: 'webapp/target', sourceFiles: '**/*war')], usePromotionTimestamp: false, useWorkspaceInPromotion: false, verbose: false)])
         sh 'ls -l'
          }
          }
       }
    }
  post {
  always {
   echo "This line will always print no matter what always"
  }
  failure {
    echo "build failed"
   }
    unstable {
      echo "Build unstable"
    }
 }
}

    
  
