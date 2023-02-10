// declare our vars outside the pipeline
def tests = [:]
//def files = ['PRB-enable-options-partA.txt', 'PRB-enable-options-partB.txt', 'PRB-enable-options-partC.txt']
def files = [ '', '--enable-all' ]

pipeline {
    agent {
        label "cloud-node"
    }
    stages {
        stage('Run Tests') {
            steps {
                script {
                    files.each { f ->
                        // add each object from the 'files' loop to the 'tests' array
                        tests[f] = {
                            node('cloud-node') {
                                echo f.toString()
                                cleanWs()
                                sh "git clone git@github.com:wolfssl/wolfssl"
                                sh "git clone git@github.com:wolfssl/testing"
                                sh "cd wolfssl && ./autogen.sh && ./configure ${f} && make"
//                                sh "cd wolfssl && ../testing/jenkins-scripts/stable/PRB/config/PRB-generic-config-parser.sh ../testing/jenkins-configure-options-files/backups/${f}"
                            }
                        }
                    }
                    // Still within the 'Script' block, run the parallel array object
                    parallel tests
                }
            }
        }
    }
}
