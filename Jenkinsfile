pipeline {
    agent {
        docker {
            image 'maven:3-alpine' 
            args '-v /root/.m2:/root/.m2 --publish 4444:4444' 
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
                sh 'mvn clean verify -Dheadless=false -Dremote=true -DseleniumGridURL=http://hub:4444/wd/hub -Dbrowser=firefox' 
            }
            post {
                always {
                    junit 'target/surefire-reports/*.xml' 
                }
            }
        }
    }
}