node{
    def maven_Home=tool  name:'maven'
    stage ('Pull from Github'){
        git branch: 'main', credentialsId: 'githubID', url: 'https://github.com/stm1510/Helloword20.git'
        git credentialsId: 'githubID', url: 'https://github.com/stm1510/hellowolrd19.git'
    }
    
    stage ('Build'){
        sh " '${maven_Home}/bin/mvn' clean install package"
    }

    stage ('Docker Build'){
        sh " docker build -t tawfiq15/xxx:${BUILD_NUMBER} . "
        sh " docker images "
    }

    stage ('Docker Login'){
        withCredentials([string(credentialsId: 'dockerpass', variable: 'dockerpass')]) {
    // some block
        sh "docker login -u tawfiq15 -p ${dockerpass}"
            
        }
        
    }

    stage ( 'Docker push'){
        sh "docker push tawfiq15/xxx:${BUILD_NUMBER}"
        
    }
    stage ('Delete images on server'){
    sh "docker rmi -f $(docker images -a -q)"
    }
}
