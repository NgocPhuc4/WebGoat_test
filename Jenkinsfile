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
                -Dsonar.host.url=http://192.168.75.131:9000 \
                -Dsonar.token=squ_de60ca0c6e63f0e558d38d7b253e62607e8a6af5'
            }
        }
        stage('OWASP Dependency-Check Vulnerabilities') {
            steps {
                dependencyCheck additionalArguments: ''' 
                            -o './'
                            -s './'
                            -f 'ALL' 
                            --prettyPrint''', odcInstallation: 'dependency-check'
                
                dependencyCheckPublisher pattern: 'dependency-check-report.xml'
      }
    }
    }
}
