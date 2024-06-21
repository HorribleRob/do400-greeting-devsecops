pipeline {
    agent { label 'nodejs' }

    // Set your OCP project
    environment { APP_NAMESPACE = 'RHT_OCP4_DEV_USER-devsecops' }

    stages{

        stage('Test'){
            steps {
                sh "node test.js"
            }
        }

        stage('Deploy') {
            steps {
                '''
                 oc start-build greeting-devsecops \
                 --follow --wait -n ${APP_NAMESPACE}
                '''
            }
        }

        stage ('Push to Quay') {
            steps {
                sh '''
                    oc start-build greeting-devsecops-quay \
                    --follow --wait -n ${APP_NAMESPACE}
                    '''
            }
        }

        // Add more stages here
    }
}
