node{
    def maven_Home=tool  name:'maven'
    stage ('Pull from Github'){
        git branch: 'main', credentialsId: 'githubID', url: 'https://github.com/stm1510/Helloword20.git'
        git credentialsId: 'githubID', url: 'https://github.com/stm1510/hellowolrd19.git'
    }
    stage ("Deploy to Kubernetes"){
    sh " aws cloudformation create-stack --stack-name tawfiq-udacity-network --region us-east-1 --parameters file://udacity-network-parameters.json --template-body file://udacity-network.yml"
    }

}
