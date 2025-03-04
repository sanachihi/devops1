pipeline {
  agent any
  tools {
    jdk 'JAVA_HOME'
    maven 'M2_HOME'
  }
  
  stages {
    stage('GIT') {
      steps {
        git branch: 'master', url: 'https://github.com/sanachihi/timesheet.git'
      }
    }
    stage('Compile Stage') {
      steps {
        sh 'mvn clean compile'
      }
    }
  stage('SonarQube Analysis') {
            steps {
                sh 'mvn sonar:sonar -Dsonar.token=sqa_9475dc01c41e81345ddaa89dbc731be725cad6d8 -Dmaven.test.skip=true';
            }
    }
   /* stage('MVN Nexus'){
    		steps {
    			sh 'mvn deploy -Dmaven.test.skip=true'
    		}
	    }*/
	  stage('Deploy Image') {
    steps {
        script {
            withDockerRegistry([credentialsId: 'docker-hub-credentials', url: '']) {
                sh '''
                    docker build -t sanachihi/timesheet-devops:1.0.0 .
                    docker push sanachihi/timesheet-devops:1.0.0
                '''
            }
        }
    }
}
  }
}
