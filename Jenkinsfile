pipeline{
    //Directives
    agent any
    // execute this pipeline in any available agent
    tools {
        maven 'maven'
    }
    // environment 
       environment {
            ArtifactID = readMavenPom().getArtifactId()
            Version = readMavenPom().getVersion()
            Name = readMavenPom().getName()
            GroupID = readMavenPom().getGroupId()
    }

    stages {
        // Specify various stage with in stages

        // stage 1. Build
        stage ('Build'){
            steps {
                sh 'mvn clean install package'
            }
        }

        // Stage2 : Testing
        stage ('Test'){
            steps {
                echo ' testing......'

            }
        }

        // Publish the artifacts to Nexus

        stage ('Publish to Nexus')
        {
            steps{
                nexusArtifactUploader artifacts: [[artifactId: 'VinayDevOpsLab', classifier: '', file: 'target/VinayDevOpsLab-0.0.4-SNAPSHOT.war', type: 'war']], credentialsId: 'd438ad00-7cb4-422b-9043-59f8f479196d', groupId: 'com.vinaysdevopslab', nexusUrl: '172.20.10.209:8081', nexusVersion: 'nexus3', protocol: 'http', repository: 'NamanDevopsLab-Snapshot', version: '0.0.4-SNAPSHOT'
            }
        }

        // Printing env variables
        stage ('Print Environment Variables') {
            steps {
                echo "${ArtifactID}"
                echo "${Version}" 
                echo "${Name}"
                echo "${GroupID}"
            }
        }

        stage ('Deploy') {
            steps {
                echo "Deploying....."
            }
        }

        // // Stage3 : Publish the source code to Sonarqube
        // stage ('Sonarqube Analysis'){
        //     steps {
        //         echo ' Source code published to Sonarqube for SCA......'
        //         withSonarQubeEnv('sonarqube'){ // You can override the credential to be used
        //              sh 'mvn sonar:sonar'
        //         }

        //     }
        // }

        
        
    }

}