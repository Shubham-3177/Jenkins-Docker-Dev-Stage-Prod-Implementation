pipeline {
    agent any

    environment {
        DEV_SERVER   = "13.239.244.37"
        STAGE_SERVER = "15.134.141.111"
        PROD_SERVER  = "54.252.66.69"
        APP_NAME = "myapp"
    }

    stages {

        stage('Deploy') {
            steps {
                script {
                    if (env.BRANCH_NAME == 'dev') {
                        deploy(DEV_SERVER, 8081)
                    }
                    else if (env.BRANCH_NAME == 'stage') {
                        deploy(STAGE_SERVER, 8082)
                    }
                    else if (env.BRANCH_NAME == 'main') {
                        deploy(PROD_SERVER, 80)
                    }
                }
            }
        }
    }
}

def deploy(server, port) {
    sh """
    ssh -o StrictHostKeyChecking=no ec2-user@${server} '
      cd /home/ec2-user
      rm -rf app || true
      git clone https://github.com/Shubham-3177/Jenkins-Docker-Dev-Stage-Prod-Implementation.git app
      cd app
      docker build -t ${APP_NAME}:${BRANCH_NAME} .
      docker rm -f ${APP_NAME} || true
      docker run -d -p ${port}:80 --name ${APP_NAME} ${APP_NAME}:${BRANCH_NAME}
    '
    """
}
