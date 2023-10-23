pipeline {
    agent any

    tools {
        // Install the Maven version configured as "M3" and add it to the path.
        maven "maven"
    }

    stages {
        stage('Build') {
            steps {
                // Run Maven on a Unix agent.
                sh "mvn spotless:apply"
                sh "mvn clean install -DskipTests"
                
            }
        }
        stage('Status Analysis - SonarQube') {
            steps {
                sh 'mvn sonar:sonar \
                -Dsonar.host.url=http://192.168.75.131/:9000 \
            }
        }
    }
}
