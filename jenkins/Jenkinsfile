// pipeline {
//     agent {
//         docker {
//             image 'maven:3-alpine'
//             args '-v /root/.m2:/root/.m2'
//         }
//     }
//     options {
//         skipStagesAfterUnstable()
//     }
//     stages {
//         stage('Build') {
//             steps {
//                 sh 'mvn -B -DskipTests clean package'
//             }
//         }
//         stage('Test') {
//             steps {
//                 sh 'mvn test -Dmaven.test.failure.ignore=true'
//             }
//             post {
//                 success {
//                     junit 'target/surefire-reports/*.xml'
//                 }
//             }
//         }
//         stage('Deliver') {
//             steps {
//                 sh './jenkins/scripts/deliver.sh'
//             }
//         }
//     }
// }

node {
    stage('Build') {
        docker.image('maven:3-alpine').inside('-v /root/.m2:/root/.m2') {
            sh 'mvn -B -DskipTests clean package'
        }
    }
    stage('Test') {
        docker.image('maven:3-alpine').inside('-v /root/.m2:/root/.m2') {
            sh 'mvn test -Dmaven.test.failure.ignore=true'
            junit 'target/surefire-reports/*.xml'
        }
    }
    stage('Deliver') {
        sh './jenkins/scripts/deliver.sh'
    }
}
