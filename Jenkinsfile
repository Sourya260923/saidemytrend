pipeline {
    agent any

    environment {
        PATH = "/opt/maven/bin:$PATH"
    }

    stages {
        stage('build') {
            steps {
                echo "---------- build started ----------"
                sh "mvn clean deploy -Dmaven.test.skip=true"
                echo "---------- build completed ----------"
            }
        }

        stage('test') {
            steps {
                echo "---------- unit test started ----------"
                sh "mvn surefire-report:report"
                echo "---------- unit test completed ----------"
            }
        }

        stage('SonarQube analysis') {
            environment {
                scannerHome = tool 'sairam-sonar-scanner'
            }
            steps {
                echo "Running SonarQube analysis..."
                sh "$scannerHome/bin/sonar-scanner"
            }
        }
    }
}
