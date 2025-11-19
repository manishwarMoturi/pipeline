# pipeline

select : in triggers --> choose --> GitHub hook trigger for GITScm polling
                                -->Poll SCM---> Schedule--> H/5 * * * *



--pipeline script
pipeline {
    agent any

    tools {
        maven 'Maven_Home'
    }

    stages {
        stage('Clone Repo & Clean') {
            steps {
                
                bat 'rmdir /s /q maven-simple'

                
                bat 'git clone https://github.com/manishwarMoturi/maven-simple.git'

               
                bat 'mvn clean -f maven-simple/pom.xml'
            }
        }

        stage('Install') {
            steps {
                bat 'mvn install -f maven-simple/pom.xml'
            }
        }

        stage('Test') {
            steps {
                bat 'mvn test -f maven-simple/pom.xml'
            }
        }

        stage('Package') {
            steps {
                bat 'mvn package -f maven-simple/pom.xml'
            }
        }
    }
}


---
