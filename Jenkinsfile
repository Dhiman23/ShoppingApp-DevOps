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
                $SCANNER_HOME/bin/sonar-scanner -Dsonar.url=http://3.91.181.203:9000/ -Dsonar.login=squ_d31a9628663bc48c1958a174f69db101a7d8942c -Dsonar.projectName=shopping-cart \
                -Dsonar.java.binaries=. \
                -Dsonar.projectKey=shopping-cart

                '''

            
        }
    }

      stage('Owasp Scan'){
            steps{
               
                  dependencyCheck additionalArguments: '--scan ./ ', odcInstallation: 'DP'
                dependencyCheckPublisher pattern: '**/dependency-check-report.xml'
               
            }
        }
        
      stage('Build application'){
            steps{
          
               
                  sh '''
                  set -x
                  mvn clean package -DskipTests=true
                  
                     '''
               
            }
        }
         stage('Build & push docker image'){
            steps{
               
                  script{
                    withDockerRegistry(credentialsId: 'docker-cred', toolName: 'docker') {
                     sh 'docker build -t shopping:latest -f docker/Dockerfile .'
                     sh 'docker tag shopping:lastest sajaldhimanitc1999/shopping:latest'
                     sh ' docker push sajaldhimanitc1999/shopping:latest'
                     }
                  }
               
            }
        }
 }

}
