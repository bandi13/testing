pipeline {
    agent none
    stages {
        stage('Run Tests') {
            parallel {
                stage('Test Enable-Options') {
                    agent {
                        label "cloud-node"
                    }
                    steps {
                        cleanWs()
                        git url: git@github.com:wolfssl/wolfssl
                        git url: git@github.com:wolfssl/testing
                        sh "ls -la"
                        sh "./autogen.sh"
                        sh ".testing/jenkins-scripts/stable/PRB/config/PRB-generic-config-parser-multithreaded.sh .testing/jenkins-configure-options-files/backups/PRB-enable-options-partA.txt"
                    }
                }
            }
        }
    }
}

