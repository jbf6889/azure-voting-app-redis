@Library('jenkins-shared-libraries@master') _

default_ms_pipeline {

DOCKER_IMAGE_NAME = 'testdockerimage'

PROJECT = 'testproject'

DEV_ENV = [
platform: 'EKS',
activated: 'yes',
runTests: 'no',
branch: "${env.BRANCH_NAME}"
]

}