pipeline {
    agent any
 
    stages {
 
        stage('Checkout') {
            steps {
                checkout scm
            }
        }
 
        stage('Publish Artifact to Exchange') {
            steps {
                bat '''
                    mvn clean deploy ^
                    -s "C:\\Users\\mahk3\\.m2\\settings.xml" ^
                    -DskipTests ^
                    -Denv=Sandbox ^
                    -Dappname=mulesoft-demo ^
                    -Dbusiness="Digicloud Solutions Pvt Ltd." ^
                    -Dtarget=Cloudhub-US-East-2 ^
                    -Dworkers=1 ^
                    -DvCore=0.1
                '''
            }
        }
 
        stage('Deploy to CloudHub 2.0') {
            steps {
 
                withCredentials([
                    usernamePassword(
                        credentialsId: 'anypoint-platform-creds',
                        usernameVariable: 'Pragati_1999',
                        passwordVariable: 'Pragati@1998'
                    )
                ]) {
 
                    bat '''
                        mvn clean deploy ^
                        -DmuleDeploy ^
                        -s "C:\\Users\\mahk3\\.m2\\settings.xml" ^
                        -DskipTests ^
                        -Danypoint.username=Pragati_1999 ^
                        -Danypoint.password=Pragati@1998 ^
                        -Denv=Sandbox ^
                        -Dappname=mulesoft-demo ^
                        -Dbusiness="Digicloud Solutions Pvt Ltd." ^
                        -Dtarget=Cloudhub-US-East-2 ^
                        -Dworkers=1 ^
                        -DvCore=0.1
                    '''
                }
            }
        }
    }
 
    post {
        success {
            echo 'Exchange publication and CloudHub 2.0 deployment completed successfully.'
        }
 
        failure {
            echo 'Pipeline failed. Check the Jenkins console log for the failed stage.'
        }
    }
}