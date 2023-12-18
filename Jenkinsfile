pipeline
{
    agent any
    stages
    {
        stage('ContinuousDownload')
        {
            steps
            {
               git 'https://github.com/intelliqittrainings/maven.git'
            }
        }
        stage('ContinuousBuild')
        {
            steps
            {
                sh 'mvn package'
            }
        }
        stage('ContinuousDeployment')
        {
            steps
            {
                deploy adapters: [tomcat9(credentialsId: '5d830073-a71c-49bf-b1d3-81ae4cb5c5db', path: '', url: 'http://172.31.17.144:8080')], contextPath: 'mytestapp', war: '**/*.war'
            }
        }
        stage('ContinuousTesting')
        {
            steps
            {
                git 'https://github.com/intelliqittrainings/FunctionalTesting.git'
                
                sh 'java -jar /home/ubuntu/.jenkins/workspace/declarativepipeline/testing.jar'
            }
        }
        stage('ContinuousDelivery')
        {
            steps
            {
                deploy adapters: [tomcat9(credentialsId: '5d830073-a71c-49bf-b1d3-81ae4cb5c5db', path: '', url: 'http://172.31.25.236:8080')], contextPath: 'myprodapp', war: '**/*.war'
            }
        }
    }
}
