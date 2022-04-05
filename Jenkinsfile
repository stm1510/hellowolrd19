pipeline {
    agent any
    triggers {
        cron('H */1 * * * ')
     }
    tools {
        maven 'maven'
      
    }
    stages {
      stage('Build'){
        steps {
          echo "Build step"
          sh 'mvn clean'
          sh 'mvn install'
          sh 'mvn package'
         
        }
      }
      
      }
        stage('test '){
        steps {
            retry(4){
          echo  "test step"
            }
          sh 'mvn test'
        }
      
      
      }
        
    
    }
    post {
        always {
            echo "Always display this message "
        }
        failure {
            echo "Job failed "
        }
        success {
            echo "Successful run "
        }
        unstable {
            echo "The job is unstable "
        }
    } 

}
