pipeline {
    agent any
    tools {
        maven "maven"
        jdk "jdk"
    }
    environment {
        ROLE_ID = credentials("role-id")
    }
    
    stages {
        stage('Initialize'){
            steps{
                echo "PATH = ${M2_HOME}/bin:${PATH}"
                echo "M2_HOME = /opt/maven"
            }
        }
        stage('Build') {
            steps {
                writeFile(file: "src/main/resources/role-id", text: "$ROLE_ID")
                dir("/var/jenkins_home/workspace/test") {
                sh 'mvn -B -DskipTests clean package'
                }
            }
        }
     }
    post {
       always {
          junit(
        allowEmptyResults: true,
        testResults: '*/test-reports/.xml'
      )
      }
   } 
}
