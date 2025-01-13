

pipeline {
    agent any
    stages {
        stage("Install") {
          steps {
            git url: 'https://github.com/cyrille-leclerc/multi-module-maven-project'
            withMaven {
              sh "mvn -Dspotbugs.skip=true -DskipTests=true clean verify"
            } // withMaven will discover the generated Maven artifacts, JUnit Surefire & FailSafe reports and FindBugs reports
          }
        }
        stage('Build') { 
            steps {
                sh 'mvn -B -Dspotbugs.skip=true -DskipTests=true clean package' 
            }
        }
        stage('Deliver') {
            steps {
                sh './jenkins/scripts/deliver.sh'
            }
        }
    }
}


