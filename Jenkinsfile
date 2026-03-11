pipeline {
    agent any
    tools {
        maven 'Maven'   // must match Global Tool Config
        jdk 'JDK'       // must match Global Tool Config
    }

    stages {
        stage('Initialize') {
            steps {
                echo "PATH = ${env.PATH}"
                echo "M2_HOME = ${env.M2_HOME}"
            }
        }
        
        stage('Build') {
            steps {
                dir("${WORKSPACE}") {
                    bat 'mvn -B -DskipTests clean package'
                }
            }
        }
    }
    
    post {
        always {
            junit(
                allowEmptyResults: true, 
                testResults: 'target/surefire-reports/*.xml'
            )
        }
    }
}
