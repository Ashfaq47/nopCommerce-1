pipeline{
    agent any
    options{
        timeout(time: 15,unit: 'MINUTES')
    }
    triggers{
        pollSCM('* * * * 1-5')
    }
    stages{
        stage('GIT'){
            steps{
                git url: 'https://github.com/Ashfaq47/nopCommerce-1.git' ,
                    branch: 'master'
            }   
        }
        stage('Build'){
            steps{
                sh 'dotnet build -c Release src/NopCommerce.sln'
                sh 'dotnet publish -c Release src/Presentation/Nop.Web/Nop.Web.csproj  -o "./published"' 
            }
            post{
                success{
                    sh 'mkdir ./published/logs ./published/bin'
                    sh 'tar -czvf nop.web.tar.gz ./published/'
                    archiveArtifacts artifacts: '**/*.tar.gz'
                }
            }
        }
    }
}