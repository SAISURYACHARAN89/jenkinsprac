pipeline{
    agent any
        environment{
            DOCKER_IMAGE = 'surya11456/jenkinsprac'
            DOCKER_CREDENTIALS_ID = 'dockerhub_credentials'
        }
        stages{
            stage('Checkout'){
                steps{
                    checkout scm
                }
            }
            stage('Build Docker image'){
                steps{
                    script{
                        dockerImage = docker.build("${DOCKER_IMAGE}:latest")
                    }
                }
            }
            stage('Push to Dockerhub'){
                steps{
                    script{
                        docker.withRegistery('https://index.docker.io/v1/',DOCKER_CREDENTIALS_ID){
                            dockerImage.push('latest')
                        }
                    }
                }
            }
        }
    post{
        success{
            echo 'image built and pushed succesfully'
        }
        failure{
            echo 'build failed'
        }
    }

}