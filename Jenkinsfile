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
            steps {
                sh 'host -t TXT pgp.michaelholley.us | awk -F \'"\' \'{print $2} \''
            }
        }
    }
}