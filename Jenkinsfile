pipeline {
    agent any
    stages {
        stage('Build') {
            steps {
                sh'mvn -B -DskipTests clean package'
            }
        }
        stage('Test') {
            steps {
                sh 'mvn test'
            }
			post {
                always {
                    junit 'target/surefire-reports/*.xml'
                }
            }
        }
        stage('Delivery') {
            steps {
                sh "sshpass -p 'vagrant' scp -o 'StrictHostKeyChecking no' target/my-app-1.0-SNAPSHOT.jar vagrant@192.168.56.104:/home/vagrant/"
                sh "sshpass -p 'vagrant' ssh -o 'StrictHostKeyChecking no' vagrant@192.168.56.104 -t 'java -jar /home/vagrant/my-app-1.0-SNAPSHOT.jar'"
            }
        }
        
        // stage('Run app') {
        //     steps {
        //         sh 'java -jar target/my-app-1.0-SNAPSHOT.jar'
        //     }
        // }
    }
}
