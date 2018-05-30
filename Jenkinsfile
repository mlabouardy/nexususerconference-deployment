def managerIp='10.0.0.34'

node('master'){
    stage('Checkout'){
        checkout scm
    }

    stage('Copy'){
        sh "scp -o StrictHostKeyChecking=no docker-compose.yml ec2-user@${managerIp}:/home/ec2-user"
    }

    stage('Test'){
        withCredentials([[$class: 'UsernamePasswordMultiBinding', credentialsId: 'registry', usernameVariable: 'USERNAME', passwordVariable: 'PASSWORD']]) {
            sh "echo $USERNAME"
            sh "echo $PASSWORD"
        }
    }

    stage('Deploy'){
        sh "ssh -oStrictHostKeyChecking=no ec2-user@${managerIp} docker login --password admin123 --username admin registry.slowcoder.com"
        sh "ssh -oStrictHostKeyChecking=no ec2-user@${managerIp} docker stack deploy --compose-file docker-compose.yml --with-registry-auth demo"
    }
}