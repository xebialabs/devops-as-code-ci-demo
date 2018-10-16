pipeline {
    agent any
    environment {
        XL_DEPLOY_URL = "http://xl-deploy:4516"
        XL_DEPLOY_CREDENTIALS = credentials("xld-credentials")
        XL_DEPLOY_USERNAME = "${env.XL_DEPLOY_CREDENTIALS_USR}"
        XL_DEPLOY_PASSWORD = "${env.XL_DEPLOY_CREDENTIALS_PSW}"

        XL_RELEASE_URL = "http://xl-release:5516"
        XL_RELEASE_CREDENTIALS = credentials("xlr-credentials")
        XL_RELEASE_USERNAME = "${env.XL_RELEASE_CREDENTIALS_USR}"
        XL_RELEASE_PASSWORD = "${env.XL_RELEASE_CREDENTIALS_PSW}"
    }

    stages {
        stage("Apply") {
            parallel {
                stage("Apply xebialabs.yaml on Linux") {
                    agent {
                        label 'master'
                    }
                    environment {
                        XL_VALUE_BUILD_NUMBER = "${currentBuild.id}"
                        XL_VALUE_RELEASE_NAME = "Pipeline for ${currentBuild.id}"
                    }

                    steps {
                        sh "./xlw apply -v -f xebialabs.yaml"
                    }
                }

                stage("Apply xebialabs.yaml on Windows") {
                    agent {
                        label 'windows'
                    }
                    environment {
                        XL_VALUE_BUILD_NUMBER = "${currentBuild.id}"
                        XL_VALUE_RELEASE_NAME = "Pipeline for ${currentBuild.id}"
                    }

                    steps {
                        bat "xlw.bat apply -v -f test.yaml"
                    }
                }
            }
        }
    }
}
