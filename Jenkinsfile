        pipeline{
            tools{
                jdk 'myjava'
                maven 'mymaven'
            }
            agent none
            stages{
                stage('Checkout on Master'){
                    agent any
                    steps{
                echo 'cloning...'
                        git 'https://github.com/adeleye1416/DevOpsCode.git'
                    }
                }
                stage('Compile on slave1'){
                    agent {label 'slave1'}
                    steps{
                        echo 'compiling...'
                        sh 'mvn compile'
                }
                }
                stage('CodeReview on slave1'){
                    agent {label 'slave1'}
                    steps{
                    
                echo 'codeReview...'
                        sh 'mvn pmd:pmd'
                    }
                }
                stage('UnitTest on slave2'){
                    agent {label 'slave2'}
                    steps{
                    echo 'Testing'
                        sh 'mvn test'
                    }
                    post {
                    success {
                        junit 'target/surefire-reports/*.xml'
                    }
                }	
                }
                stage('Package on Master'){
                    agent any
                    steps{
                        sh 'mvn package'
                    }
                }
            }
        }

