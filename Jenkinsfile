pipeline {
    agent any
    tools {
        maven "Maven3"
    }
    stages {
        stage('Github clone') { 
            steps {
                checkout([$class: 'GitSCM', branches: [[name: '*/main']], extensions: [], userRemoteConfigs: [[credentialsId: 'githubid', url: 'https://github.com/KameshvaranV/myproduction-repo']]]) 
            }
        }
        stage ("Build") {
            steps {
                sh "mvn clean install -f MyWebApp/pom.xml"
            }
            
        }
        stage ("Deploy") {
            steps {
                deploy adapters: [tomcat8(credentialsId: 'tomcat_id', path: '', url: 'http://54.226.140.86:9090/')], contextPath: null, war: '**/*.war'
            }
        }

    }
    
}
