pipeline {
    agent any

    environment {
        DEV_SERVER   = "3.106.214.26"
        STAGE_SERVER = "3.24.123.30"
        PROD_SERVER  = "3.107.69.57"
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
