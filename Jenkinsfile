pipeline {
    agent none

    environment {
      REGION = ''
      REGISTRY = ''
      BUCKET = ''
      DB_NAME = ''
      DB_USER = ''
      DB_URL = ''
      DB_PORT = ''
      CLUSTER = ''
    }


    stages {
        stage('build-main') {
          agent {
            label 'foxtrot_build'
          }
            steps {
              echo "=========== BUILD APP ============"
                git branch: 'main',
                  credentialsId: 'avramenko',
                   url: '${URL}'
              sh '''
               chmod 777 script-DSL/build_app.sh && script-DSL/build_app.sh
                  '''
              echo "============== PUSH INTO REGISTRY ============"
              sh '''
              chmod 777 script-DSL/push_registry.sh && script-DSL/push_registry.sh
               '''
                }
              }
              stage ('deploy') {
                agent {
                  label 'foxtrot_deploy'
                }
                steps {
                       git branch: 'main',
                        credentialsId: 'avramenko',
                        url: '${URL}'
                  echo "============ DEPLOY APP ============="
                sh '''
                chmod 777 script-DSL/deploy.sh && script-DSL/deploy.sh
                  '''
                }
          }
    }
}