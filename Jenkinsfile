pipeline{
    agent{label 'master'}
    tools{
        maven 'M3'
    }
    stages{
        stage('Checkout'){
            steps{
                git 'https://github.com/AnjuMeleth/spring-petclinic.git'
            }
        }
        stage('Build'){
            steps{
                 sh 'mvn clean compile'
            }
        }
        stage('Test'){
            steps{
                     sh 'mvn test'
                     junit '**/target/surefire-reports/TEST-*.xml'
            }
        }
        stage('Package'){
            steps{
                sh 'mvn package'
                archiveArtifacts artifacts: 'target/*.jar', fingerprint: true
            }
        }
        stage('Deploy'){
            steps{
                input 'Do you approve the deployment?'
                sh 'scp target/*.jar deploy1@45.76.161.96:/home/deploy1'
                sh "ssh deploy1@45.76.161.96 'nohup java -jar /home/deploy1/spring-petclinic-2.1.0.BUILD-SNAPSHOT.jar &'"
            }
        }
    }
}