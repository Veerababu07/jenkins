pipeline 
     agent any
    triggers { ('*/10 * * * *') }
    stages {
        stage ('vcs'){
            steps {
               git url : 'https://github.com/Veerababu07/spring-petclinic.git',
                 branch : 'main'
            }
        }
        stage ('build') {
            steps {
               sh 'mvn package'
               sh 'mvn clean install'
            }
        }
        stage ('artifacts') {
            stage('Artifactory-Configuration') {
            steps {
               rtServer (
                    id: "JFROG_OCT22",
                    url: "https://qtdevopsoct22.jfrog.io/",
                    credentialsId: "JFROG_ADMIN_ID"
                )
            }    
        }
        stage ('artifacts results') {
            steps {
                junit '**/surefire-reports/*.xml'
            }
          }
    }
}
