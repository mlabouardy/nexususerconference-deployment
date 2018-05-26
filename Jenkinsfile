def managerIp='10.0.2.94'

node('master'){
    stage('Checkout'){
        checkout scm
    }

    stage('Copy'){
        sh "scp -o StrictHostKeyChecking=no docker-compose.yml ec2-user@${managerIp}:/home/ec2-user"
    }

    stage('Deploy'){
        sh "ssh -oStrictHostKeyChecking=no ec2-user@${managerIp} docker stack deploy --compose-file docker-compose.yml --with-registry-auth demo"
    }
}