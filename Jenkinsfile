pipeline{
    
    agent any
    
    stages {
        
        stage('Git Checkout'){
            
            steps{
                
                script{
                    
                    git branch: 'main', url: 'https://github.com/Mbianda2022/mrdevops_java_app.git'
                    
                }
            }
        }
        stage('Unit testing'){
            
            steps{
                
                script{
                    
                    sh 'mvn test'
                    
                }
            }
        }
        stage('Itegration testing'){
            
            steps{
                
                script{
                    
                    sh 'mvn verify -DskipUnitTests'
                    
                }
            }
        }
        stage('Maven Build'){
            
            steps{
                
                script{
                    
                    sh 'mvn clean install'
                    
                }
            }
        }
        stage('Static code analysis'){
            
            steps{
                
                script{
                    
                 withSonarQubeEnv(credentialsId: 'sonar-api') {
                             
                      sh 'mvn clean package sonar:sonar'

                   }
                    
                }
            }
        }
        stage('Quality Gate Status'){
            
            steps{
                
                script{
                    
                    waitForQualityGate abortPipeline: false, credentialsId: 'sonar-api'
                }
            }
        }
        stage('nexus artifact uploader'){

            steps{

                script{
                   
               nexusArtifactUploader artifacts: 
               [
                  [
                     artifactId: 'springboot', 
                     classifier: '', 
                     file: 'target/Uber.jar', 
                     type: 'jar'
                    ]
                ], 
                credentialsId: 'nexus-newcreds', 
                groupId: 'com.example', 
                nexusUrl: '44.201.155.173:8081', 
                nexusVersion: 'nexus3', 
                protocol: 'http', 
                repository: 'cloudlord-releases', 
                version: '1.0.0'
                }
            }
        }


        }
     }
   
