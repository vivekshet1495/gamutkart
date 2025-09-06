pipeline{
    agent any
    tools{
        maven 'maven'
    }
    stages{
        stage("clone"){
            steps{
            git changelog: false, poll: false, url: 'https://github.com/vivekshet1495/gamutkart.git'
            }
        }
        stage("build-repo"){
            steps{
                sh 'mvn install -D maven.test.skip=true'
            }
        }
        stage("build-test-ready"){
            steps{
                sh 'mvn compiler:testCompile'
                sh 'mvn surefire:test'
                junit 'target/**/*.xml'
            }
        }
        stage("deployment"){
            steps{
            sh '''scp target/gamutkart.war vivek@13.127.159.105:/home/vivek/tomcat/webapps/
ssh vivek@13.127.159.105 "tomcat/bin/startup.sh"'''
            }
        }
    }
}
