pipeline {

    agent any
    tools {
        maven 'mvn' 
    }
    stages {
        stage('Compile stage') {
            steps {
                sh "mvn clean install" 
        }
    }

         stage('testing stage') {
             steps {
                sh "mvn test"
        }
    }
	  
	stage('build && SonarQube analysis') {
         steps {
              withSonarQubeEnv('sonarqube') {
                    // Optionally use a Maven environment you've configured already
              sh 'mvn clean install sonar:sonar'
             }
        }
     }

        stage('Deploy') {
            steps {
                sh "scp -r /root/.jenkins/workspace/declpipeline/in28minutes-web-servlet-jsp/target/*.war root@10.0.0.5:/opt/apache-tomcat-8.5.50/webapps/"
            }
        }

  }

}
