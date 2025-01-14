pipeline {
    agent {
        docker {
            image 'maven:3.9.0'
            args '-v /root/.m2:/root/.m2'
        }
    }
    stages {
        stage('Build') {
            steps {
                sh 'mvn -B -DskipTests clean package'
            }
        }
        stage('Test') {
            steps {
                sh 'mvn test'
            }
            post {
                always {
                    junit 'target/surefire-reports/*.xml'
                }
            }
        }
        stage('Deliver') {
            steps {
                sh './jenkins/scripts/deliver.sh'
            }
        }
    }
}
/*
pipeline {
    agent any
    options {
        skipStagesAfterUnstable()
    }
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
                sh '''
                    echo 'The following Maven command installs your Maven-built Java application'
                    echo 'into the local Maven repository, which will ultimately be stored in'
                    echo 'Jenkins''s local Maven repository (and the "maven-repository" Docker data'
                    echo 'volume).'
                    set -x
                    mvn jar:jar install:install help:evaluate -Dexpression=project.name
                    set +x
                    
                    echo 'The following command extracts the value of the <name/> element'
                    echo 'within <project/> of your Java/Maven project''s "pom.xml" file.'
                    set -x
                    NAME=`mvn -q -DforceStdout help:evaluate -Dexpression=project.name`
                    set +x
                    
                    echo 'The following command behaves similarly to the previous one but'
                    echo 'extracts the value of the <version/> element within <project/> instead.'
                    set -x
                    VERSION=`mvn -q -DforceStdout help:evaluate -Dexpression=project.version`
                    set +x
                    
                    echo 'The following command runs and outputs the execution of your Java'
                    echo 'application (which Jenkins built using Maven) to the Jenkins UI.'
                    set -x
                    java -jar demo-1/target/demo-1-0.0.30-SNAPSHOT.jar
                '''
            }
        }
       
    }
}

 */
