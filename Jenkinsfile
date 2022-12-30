pipeline{
    agent any
    tools{
        maven 'Maven For Pipeline Build'

    }
    stages{
        stage('build maven')
        {
            steps{
                checkout([$class: 'GitSCM', branches: [[name: '*/master']], extensions: [], userRemoteConfigs: [[credentialsId: 'a0f2a992-321e-4e0e-a9fa-683be395ec81', url: 'https://github.com/hoanglap/CICDPractice']]])            
                sh 'mvn clean install'
            }
        }
        stage('test')
        {
            steps{
                sh 'mvn test'
            }
        }
        stage('build docker image')
        {
            steps{
                script{
                sh 'docker build -t lapnguyen/cicdpractice .'
                }
            }
        }
   stage('push docker image')
        {
            steps{
                script{
	withCredentials([string(credentialsId: 'dockerpassword', variable: 'dockerpassword')]) {
    		sh 'docker login -u hoanglap93@gmail.com -p nHl@12021993'
}
		sh 'docker push lapnguyen/cicdpractice'
                }
            }
        }

    }
    
}