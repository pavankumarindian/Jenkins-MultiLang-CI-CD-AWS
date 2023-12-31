pipeline {
    agent {
        label 'ubuntu-agent'
    }

    stages {
        stage('Checkout from GitHub') {
            steps {
                script {
                    // Assuming your GitHub credentials are configured in Jenkins
                    checkout([$class: 'GitSCM', branches: [[name: '*/main']], userRemoteConfigs: [[url: 'https://github.com/your-username/my-java-web-app.git']]])
                    checkout([$class: 'GitSCM', branches: [[name: '*/main']], userRemoteConfigs: [[url: 'https://github.com/your-username/my-java-web-app-gradle.git']]])
                    checkout([$class: 'GitSCM', branches: [[name: '*/main']], userRemoteConfigs: [[url: 'https://github.com/your-username/my-python-web-app.git']]])
                    checkout([$class: 'GitSCM', branches: [[name: '*/main']], userRemoteConfigs: [[url: 'https://github.com/your-username/my-dotnet-web-app.git']]])
                }
            }
        }

        stage('Install Maven') {
            steps {
                script {
                    sh 'sudo apt-get update && sudo apt-get install -y maven'
                }
            }
        }

        stage('Build and Deploy Java App with Maven') {
            steps {
                script {
                    sh 'mvn clean install'
                    sh 'docker build -t my-java-web-app:latest -f Dockerfile-java .'
                    sh 'scp -o StrictHostKeyChecking=no -i /path/to/key.pem target/app.jar ubuntu@<java-ec2-instance-ip>:/path/to/destination'
                    sh 'ssh -o StrictHostKeyChecking=no -i /path/to/key.pem ubuntu@<java-ec2-instance-ip> "docker run -d -p 8080:8080 my-java-web-app:latest"'
                }
            }
        }

        stage('Install Gradle') {
            steps {
                script {
                    sh 'sudo apt-get install -y gradle'
                }
            }
        }

        stage('Build and Deploy Java App with Gradle') {
            steps {
                script {
                    sh 'gradle build'
                    sh 'docker build -t my-java-web-app-gradle:latest -f Dockerfile-gradle .'
                    sh 'scp -o StrictHostKeyChecking=no -i /path/to/key.pem build/libs/app.jar ubuntu@<gradle-ec2-instance-ip>:/path/to/destination'
                    sh 'ssh -o StrictHostKeyChecking=no -i /path/to/key.pem ubuntu@<gradle-ec2-instance-ip> "docker run -d -p 8081:8080 my-java-web-app-gradle:latest"'
                }
            }
        }

        stage('Install Python Build Tool') {
            steps {
                script {
                    sh 'sudo apt-get install -y python3 python3-pip'
                    sh 'pip3 install -r requirements.txt'
                }
            }
        }

        stage('Build and Deploy Python App') {
            steps {
                script {
                    sh 'echo "print(\'Hello, Python!\')" > app.py'
                    sh 'docker build -t my-python-web-app:latest -f Dockerfile-python .'
                    sh 'scp -o StrictHostKeyChecking=no -i /path/to/key.pem target/app.py ubuntu@<python-ec2-instance-ip>:/path/to/destination'
                    sh 'ssh -o StrictHostKeyChecking=no -i /path/to/key.pem ubuntu@<python-ec2-instance-ip> "docker run -d -p 5000:5000 my-python-web-app:latest"'
                }
            }
        }

        stage('Install .NET Build Tool') {
            steps {
                script {
                    sh 'sudo apt-get update && sudo apt-get install -y dotnet-sdk-3.1'
                }
            }
        }

        stage('Build and Deploy .NET App') {
            steps {
                script {
                    sh 'echo "Console.WriteLine(\'Hello, .NET!\')" > Program.cs'
                    sh 'dotnet build'
                    sh 'docker build -t my-dotnet-web-app:latest -f Dockerfile-dotnet .'
                    sh 'scp -o StrictHostKeyChecking=no -i /path/to/key.pem bin/Debug/netcoreapp3.1/app.dll ubuntu@<dotnet-ec2-instance-ip>:/path/to/destination'
                    sh 'ssh -o StrictHostKeyChecking=no -i /path/to/key.pem ubuntu@<dotnet-ec2-instance-ip> "docker run -d -p 8082:80 my-dotnet-web-app:latest"'
                }
            }
        }
    }
}
