pipeline {

    agent any

    stages {
        stage("Apply xebialabs.yaml") {
            steps {
                withCredentials([usernamePassword(credentialsId: 'xld-credentials', usernameVariable: 'xld_username', passwordVariable: 'xld_password')]) {
                    withCredentials([usernamePassword(credentialsId: 'xlr-credentials', usernameVariable: 'xlr_username', passwordVariable: 'xlr_password')]) {
                        sh "./xlw apply -v -f xebialabs.yaml --xl-deploy-url http://xl-deploy:4516 --xl-deploy-username ${xld_username} --xl-deploy-password ${xld_password} --xl-release-url http://xl-release:5516 --xl-release-username ${xlr_username} --xl-release-password ${xlr_password} --values build.number=${currentBuild.id},release.name=\"Pipeline for ${currentBuild.id}\""
                    }
                }
            }
        }
    }

}
