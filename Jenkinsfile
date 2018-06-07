def managerIp = '10.0.0.179'
def registry = 'registry.slowcoder.com'

node('master'){
    stage('Checkout'){
        checkout scm
    }

    stage('Copy'){
        sh "scp -o StrictHostKeyChecking=no docker-compose.yml ec2-user@${managerIp}:/home/ec2-user"
    }

    stage('Deploy'){
        withCredentials([[$class: 'UsernamePasswordMultiBinding', credentialsId: 'registry', usernameVariable: 'USERNAME', passwordVariable: 'PASSWORD']]) {
            sh "ssh -oStrictHostKeyChecking=no ec2-user@${managerIp} docker login --password $PASSWORD --username $USERNAME ${registry}"
            sh "ssh -oStrictHostKeyChecking=no ec2-user@${managerIp} docker stack deploy --compose-file docker-compose.yml --with-registry-auth demo"
        }
    }
}