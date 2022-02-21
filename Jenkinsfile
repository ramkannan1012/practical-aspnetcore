pipeline {
    agent {label 'slave'}
  
    stages {
        stage('initialize') {
            steps {
                sh '''
                        export CODEARTIFACT_AUTH_TOKEN=`aws codeartifact get-authorization-token --domain nudom --domain-owner 678876462442 --query authorizationToken --output text`
                   
                   '''
            }
        }
        stage('Build'){
            steps{
                sh '''
                        cd /home/ubuntu/netproject/practical-aspnetcore/projects/application-environment/
                        dotnet build application-environment.csproj
                        
                   '''
               
            }
            
        }
        stage('pushartifacts to AWS') {
            steps {
                sh '''
                        cd /home/ubuntu/netproject/practical-aspnetcore/projects/application-environment/
                        dotnet pack -p:Version=$BUILD_NUMBER application-environment.csproj -o publish/
                        dotnet nuget push publish/ -s nudom/nu-repo
                   '''
                        
                }
           }
      }
}
