pipeline {
    agent {label "aws-label" }
    // agent any

    tools {
        // Install the Maven version configured as "M3" and add it to the path.
        maven "mvn_3.9.6"
    }

    stages {
        stage('Build') {
            steps {
                // Get some code from a GitHub repository
                // git 'https://github.com/sivagurunathbabu/webapp.git'
                checkout scm

                // Run Maven on a Unix agent.
                sh "mvn -Dmaven.test.failure.ignore=true clean package"

                // To run Maven on a Windows agent, use
                // bat "mvn -Dmaven.test.failure.ignore=true clean package"
            }


           
        }

        stage('Sonar Qube') {
           steps {
                     withSonarQubeEnv('sonarQube') {
                          sh "mvn clean verify sonar:sonar -Dsonar.projectKey=myapp"
                      }
          
                 }
        }
    }
}
