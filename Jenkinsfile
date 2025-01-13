

pipeline {
    agent any
    stages {
        stage("Install") {
          steps {
            git url: 'https://github.com/cyrille-leclerc/multi-module-maven-project'
            withMaven {
              findbugsPublisher(disabled: true)
              sh "mvn clean verify"
            } // withMaven will discover the generated Maven artifacts, JUnit Surefire & FailSafe reports and FindBugs reports
          }
        }
        stage('Build') { 
            steps {
                sh 'mvn -B -DskipTests clean package' 
            }
        }
    }
}

