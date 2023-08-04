pipeline {
    agent any

    stages {
        stage('Git checkout'){
            steps {
               scripts{
                   git 'https://github.com/Dhiman23/ShoppingApp-DevOps.git'
                   branch: main
               }
            }
        }
    }
}
