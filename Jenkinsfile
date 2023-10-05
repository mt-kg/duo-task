pipeline{
        agent any
        stages{
            stage('Build docker images on Jenkins'){
                steps{
                    sh '''
                    docker build -t mtkg/duo-nginx:latest ./nginx
                    docker build -t mtkg/duo-flask:latest .
                    '''
                }
            }
            stage('Push images to Docker Hub'){
                steps{
                    sh '''
                    docker push mtkg/duo-nginx:latest
                    docker push mtkg/duo-flask:latest
                    '''
                }
            }
            stage('Run a rollout restart'){
                steps{
                    sh '''
                    kubectl apply -f .
                    kubectl rollout restart deployment flask-deployment
                    '''
                }
            }
        }
}