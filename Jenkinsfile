pipeline {
    agent {
        docker {
            image 'maven:3-alpine' 
            args '-v /root/.m2:/root/.m2 --network jenkins' 
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
                sh '''
                    mvn clean verify -Dheadless=false -Dremote=true -DseleniumGridURL=http://hub:4444/wd/hub -Dbrowser=firefox
                    mvn clean verify -Dheadless=false -Dremote=true -DseleniumGridURL=http://hub:4444/wd/hub -Dbrowser=chrome
                   '''
            }
        }
    }
}