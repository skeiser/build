pipeline {
    agent none
    environment {
        NODE_VER = '8.1.0'
    }

    stages {
        stage ('Beginning') { agent any
        environment {
            NEW_VAR = 'Howdy'
        }
            steps {
                echo 'Hello World'
                sh 'echo $NODE_VER'
                echo "@{env.NEW_VAR}"
            } 
        }

        stage ('Who am I>') { agent any
            environment {
                    DEPLOY_VERSION = 'prod'
            }
            steps {   
                echo "${env.DEPLOY_VERSION}"
                sh 'host -t TXT pgp.michaelholley.us | awk -F \'"\' \'{print $2} \''
            }
        }
        stage('Deploy to stage?') { agent none
            when {
                anyOf {
                    branch 'stage'
                    environment name: 'NODE_VER', value '8.1.0'
                }
            }
            steps {
                input 'Deploy to stage?' 
            }
        }

        stage ('Parallel') {
            failFast true
            parallel {
                stage('Build 1') { agent any
                    steps {
                        echo "It's ME!!"
                    }
                }

                stage ('Build 2') { agent any
                    steps {
                        echo "No, it's me!!"
                    }
                    
                }
            }
        }
    }
}