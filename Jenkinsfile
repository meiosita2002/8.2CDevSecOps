pipeline {
    agent any

    environment {
        SONAR_TOKEN = credentials('SONAR_TOKEN')
    }

    stages {
        stage('Checkout') {
            steps {
                git branch: 'main', url: 'https://github.com/meiosita2002/8.2CDevSecOps.git'
            }
        }

        stage('Install Dependencies') {
            steps {
                sh 'npm install'
            }
        }

        stage('Run Tests') {
            steps {
                sh 'npm test || true'
            }
        }

        stage('Generate Coverage Report') {
            steps {
                sh 'npm run coverage || true'
            }
        }

        stage('NPM Audit (Security Scan)') {
            steps {
                sh 'npm audit || true'
            }
        }

        stage('SonarCloud Analysis') {
            steps {
                sh '''
                    if [ ! -d sonar-scanner ]; then
                        curl -fsSL -o sonar-scanner-cli.zip https://binaries.sonarsource.com/Distribution/sonar-scanner-cli/sonar-scanner-cli-5.0.1.3006-linux.zip
                        unzip -q sonar-scanner-cli.zip
                        mv sonar-scanner-5.0.1.3006-linux sonar-scanner
                    fi

                    if [ ! -d jdk-21 ]; then
                        curl -fsSL -o jdk21.tar.gz https://github.com/adoptium/temurin21-binaries/releases/download/jdk-21.0.4%2B7/OpenJDK21U-jdk_x64_linux_hotspot_21.0.4_7.tar.gz
                        mkdir -p jdk-21
                        tar -xzf jdk21.tar.gz -C jdk-21 --strip-components=1
                    fi

                    export JAVA_HOME=$(pwd)/jdk-21
                    export PATH=$JAVA_HOME/bin:$PATH
                    java -version

                    ./sonar-scanner/bin/sonar-scanner -Dsonar.login=$SONAR_TOKEN
                '''
            }
        }
    }
}
