pipeline {
    agent any
    
    tools {
        // These names must match what you configured in Global Tool Configuration
        maven "MAVEN" 
        jdk "JDK"
    }

    stages {
        stage('Initialize') {
            steps {
                // On Windows, use 'bat' and Windows environment variable syntax
                echo "PATH = ${M2_HOME}/bin:${PATH}"
                echo "M2_HOME = /opt/maven"
            }
        }
        
        stage('Build') {
            steps {
                dir("/var/lib/jenkins/workspace/demopipelinetask"){              
                // inside your workspace folder by default.
                 'mvn -B -DskipTests clean package'
                }
            }
        }
    }
    
    post {
        always {
            // Updated pattern to standard Maven surefire report location
            junit(
                allowEmptyResults: true, 
                testResults: '*/test-reports/.xml'
            )
        }
    }
}
