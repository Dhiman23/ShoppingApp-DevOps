pipeline {
    agent any
    tools{
        jdk  'jdk11'
        maven 'maven3'
    }
    environment{
        SCANNER_HOME= tool 'sonar-scanner'
    }

    stages {
        stage('Git checkout'){
            steps {
              
                  git branch: 'main', changelog: false, poll: false, url: 'https://github.com/Dhiman23/ShoppingApp-DevOps.git'
               
            }
        }
    
        stage('compile'){
            steps{
               
                    sh 'mvn clean compile'
               
            }
        }
        stage('sonnar-Qube Analysis'){
        steps{
           
                sh'''
                $SCANNER_HOME/bin/sonar-scanner -Dsonar.url=http://3.95.168.122:9000/ -Dsonar.login=squ_d31a9628663bc48c1958a174f69db101a7d8942c -Dsonar.projectName=shopping-cart \
                -Dsonar.java.binaries=. \
                -Dsonar.projectkey=shopping-cart

                '''

            
        }
    }
 }

}
