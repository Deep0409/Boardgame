pipeline {
    agent any

    environment {
        SONAR_HOME = tool "Sonar"
        IMAGE_NAME = '891612555058.dkr.ecr.us-east-1.amazonaws.com/board-game'
        IMAGE_TAG = 'latest'
        FULL_IMAGE_NAME = "${IMAGE_NAME}:${IMAGE_TAG}"
        KUBECONFIG = credentials('k8s-creds')
        NEXUS_URL = 'http://34.224.53.214:8081/repository/maven-releases-board-game/'
    }

    stages {

        stage("Clone Code From GitHub") {
            steps {
                git url: 'https://github.com/Deep0409/Boardgame.git', branch: 'main'
            }
        }

        stage("Static Code Analysis (SonarQube)") {
            steps {
                withSonarQubeEnv('Sonar') {
                    sh """
                        ${SONAR_HOME}/bin/sonar-scanner \
                        -Dsonar.projectKey=Boardgame \
                        -Dsonar.projectName=Boardgame \
                        -Dsonar.sources=.
                    """
                }
            }
        }

        stage("OWASP Dependency Check") {
            steps {
                dependencyCheck additionalArguments: '--scan ./ --disableCentral', odcInstallation: 'dc'
                dependencyCheckPublisher pattern: '**/dependency-check-report.xml'
            }
        }

        stage("Sonar Quality Gate") {
            steps {
                timeout(time: 4, unit: 'MINUTES') {
                    waitForQualityGate abortPipeline: true
                }
            }
        }

        stage("Build with Maven") {
            steps {
                sh 'mvn clean package -DskipTests'
            }
        }

        stage("Authenticate to ECR") {
            steps {
                sh """
                    aws ecr get-login-password --region us-east-1 | \
                    docker login --username AWS --password-stdin 891612555058.dkr.ecr.us-east-1.amazonaws.com
                """
            }
        }

        stage("Docker Build and Push to ECR") {
            steps {
                sh """
                    docker build -t ${FULL_IMAGE_NAME} .
                    docker push ${FULL_IMAGE_NAME}
                """
            }
        }

        stage("Scan Docker Image (Trivy)") {
            steps {
                sh "trivy image ${FULL_IMAGE_NAME}"
            }
        }

        stage("Deploy to Kubernetes") {
            steps {
                sh """
                    kubectl apply -f ./board-game-deployment.yaml
                    kubectl apply -f ./deployment-service.yaml
                """
            }
        }
    }

    post {
        always {
            echo "Cleaning up local resources..."

            sh '''
                docker rmi -f ${FULL_IMAGE_NAME} || true
                docker rmi -f board-game:latest || true
                mvn clean || true
                rm -rf target/ .scannerwork/ dependency-check-report.xml || true
            '''
        }
    }
}
