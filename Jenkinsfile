pipeline {
     agent any
     tools {
        // Install the Maven version configured as "M3" and add it to the path.
        maven "MVN_HOME"
    }
    stages {
        stage('Static Analysis') {
            steps {
                echo 'Run the static analysis to the code' 
            }
        }
        stage('Compile') {
            steps {
                echo 'Compile the source code'
                bat "mvn -Dmaven.test.failure.ignore=true clean package"
            }
            post {
                always{
                    emailext body: 'The pipeline has failed, please go to Jenkins and check the problem', subject: 'Pipeline status', to: 'emileastih1@gmail.com'
                }
                success {
                    junit '**/target/surefire-reports/TEST-*.xml'
                    archiveArtifacts 'target/*.jar'
                }
            }
        }
        stage('Security Check') {
            steps {
                echo 'Run the security check against the application' 
            }
        }
        stage('Run Unit Tests') {
            steps {
                echo 'Run unit tests from the source code' 
            }
        }
        stage('Run Integration Tests') {
            steps {
                echo 'Run only crucial integration tests from the source code' 
            }
        }
        stage('Publish Artifacts') {
            steps {
                //input("Do you want to continue or not?")
                echo 'Save the assemblies generated from the compilation' 
              // deploy adapters: [tomcat9(credentialsId: '1ce22c72-db05-4750-a319-41e077da87bf', path: '', url: 'http://localhost:8088')], contextPath: 'anything', war: '**/*.war'
            }
        }
    }
}
