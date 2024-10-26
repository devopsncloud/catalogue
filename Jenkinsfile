pipeline {
    agent {
    node {
        label 'AGENT-1'
        
    }
}

environment { 
    packageVersion = ''
    nexusURL = '172.31.39.170:8081'
    }

    options {
                timeout(time: 1, unit: 'HOURS') 
                disableConcurrentBuilds() 
    }

     parameters {
    //     string(name: 'PERSON', defaultValue: 'Jenkins', description: 'Who should I say hello to?')

    //     text(name: 'BIOGRAPHY', defaultValue: '', description: 'Enter some information about the person')

        booleanParam(name: 'Deploy', defaultValue: false, description: 'Toggle this value')

    //     choice(name: 'CHOICE', choices: ['One', 'Two', 'Three'], description: 'Pick something')

    //     password(name: 'PASSWORD', defaultValue: 'SECRET', description: 'Enter a password')
     }

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
