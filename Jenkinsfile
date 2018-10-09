pipeline {

    agent any

    environment {
        XL_DEPLOY_URL = "http://xl-deploy:4516"
        XL_RELEASE_URL = "http://xl-release:5516"
    }

    stages {
        stage("Apply xebialabs.yaml") {
            environment {
                XL_VALUE_BUILD_NUMBER = "${currentBuild.id}"
                XL_VALUE_RELEASE_NAME = "Pipeline for ${currentBuild.id}"
            }

            steps {
                withCredentials([usernamePassword(credentialsId: 'xld-credentials', usernameVariable: 'xld_username', passwordVariable: 'xld_password')]) {
                    withCredentials([usernamePassword(credentialsId: 'xlr-credentials', usernameVariable: 'xlr_username', passwordVariable: 'xlr_password')]) {
                        sh "./xlw apply -v -f xebialabs.yaml --xl-deploy-username ${xld_username} --xl-deploy-password ${xld_password} --xl-release-username ${xlr_username} --xl-release-password ${xlr_password}"
                    }
                }
            }
        }
    }

}
