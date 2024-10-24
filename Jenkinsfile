pipeline {
    agent {
    node {
        label 'AGENT-1'
        
    }
}

environment { 
    packageVersion = ''
    nexusURL = '54.221.135.237'
    }

    options {
                timeout(time: 1, unit: 'HOURS') 
                disableConcurrentBuilds() 
    }

    // parameters {
    //     string(name: 'PERSON', defaultValue: 'Jenkins', description: 'Who should I say hello to?')

    //     text(name: 'BIOGRAPHY', defaultValue: '', description: 'Enter some information about the person')

    //     booleanParam(name: 'TOGGLE', defaultValue: true, description: 'Toggle this value')

    //     choice(name: 'CHOICE', choices: ['One', 'Two', 'Three'], description: 'Pick something')

    //     password(name: 'PASSWORD', defaultValue: 'SECRET', description: 'Enter a password')
    // }

    stages {
        stage('Get the version from json file') {
            steps {
                script{
                    def packageJson = readJSON file: 'package.json'
                    packageVersion = packageJson.version
                    echo "package version is: ${packageVersion}"
                }
            }
        }
        stage('Install Dependencies') {
            steps {
                sh """
                    npm install 
                """
            }
        }

        stage('Build') {
            steps {
                sh """
                    ls -la
                    zip -q -r catalogue.zip ./* -x ".git" -x "*.zip"
                    ls -ltr
                """
            }
        }

        stage('Publish artifact to Nexus') {
            steps {
                nexusArtifactUploader(
                    nexusVersion: 'nexus3',
                    protocol: 'http',
                    nexusUrl: '${nexusURL}',
                    groupId: 'com.roboshop',
                    version: ${packageVersion},
                    repository: 'catalogue',
                    credentialsId: 'nexus-creds',
                    artifacts: [
                        [artifactId: catalogue,
                        classifier: '',
                        file: 'catalogue.zip',
                        type: 'zip']
                    ]
                )
            }
        }


        stage('Deploy') {
            steps {
                sh '''
                echo "We can write shell script here"
                #env
                #sleep 10
                '''
            }
        }

//         stage('Checking Parameters usage') {
//             steps{
//                  sh """
//                     echo "Hello ${params.PERSON}"

//                     echo "Biography: ${params.BIOGRAPHY}"

//                     echo "Toggle: ${params.TOGGLE}"

//                     echo "Choice: ${params.CHOICE}"

//                     echo "Password: ${params.PASSWORD}"

//         """
//     }
// }
}



    post { 
        always { 
            echo 'I will always say Hello again!'
            deleteDir()
        }

        success { 
            echo 'The Job has ran  successfully!'
        }

        failure { 
            echo 'Useful when alerts has to send upon failure'
        }
    }
}
