pipeline {
    agent { label 'MAVEN' 
    }
    
    options { timeout(time: 30, unit: 'MINUTES')}

    triggers { pollSCM ('* * * * *')}

   
stages 

{

    stage('git') {

        steps {

       git url : 'https://github.com/nagendhrakothapalli/spring-petclinic.git',
       branch : 'dev'
        }
    }

    stage('build') {

        steps {

            sh 'mvn clean package'
            }
            post {

                success {
             archiveArtifacts artifacts: '**/spring-petclinic-*.jar'
             junit testResults: '**/TEST-*.xml'
             mail subject: 'Build stage succeed',
             from: 'nagendhra.kothapalli@gmail.com',
             to: 'kothapallinagenddrra@gmail.com',
             body: "Refer to $BUILD_URL for more details"

                }

             failure {
              mail subject: 'Build stage succeed',
             from: 'nagendhra.kothapalli@gmail.com',
             to: 'kothapallinagenddrra@gmail.com',
             body: "Refer to $BUILD_URL for more details"

                }
    
            }
            

        }
}

}