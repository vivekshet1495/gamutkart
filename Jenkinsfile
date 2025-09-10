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
        stage("build-test"){
            steps{
                sh 'mvn compiler:testCompile'
            }
        }
        stage("Test-Result"){
            steps{
                sh 'mvn surefire:test'
                junit 'target/**/*.xml'
            }
        }
        stage("deployment"){
            steps{
                sh 'touch /var/lib/jenkins/.ssh/known_hosts'
                sh 'ssh-keyscan -H 13.127.159.105 >> /var/lib/jenkins/.ssh/known_hosts'
                sh 'scp -r target/gamutkart.war vivek@13.127.159.105:/home/vivek/tomcat/webapps/'
                sh 'ssh vivek@13.127.159.105 "tomcat/bin/startup.sh"'
            }
        }
    }
}
