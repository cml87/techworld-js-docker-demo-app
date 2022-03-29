pipeline {

    // CODE_CHANGES = gitChangesQ();   // this will be a groovy script that will determine whether there were code changes or not 
                                       // in the code base we are building with this pipeline. It will return a boolean. We'll use 
                                       // this variable later, in the condition for the stages.  
    
    agent any

    // custom environment variables for this pipeline
    environment {
        NEW_VERSION = '1.3.0'
        // SERVER_CREDENTIALS = credentials('my-server-credentials')
    }

    stages {

        stage("build") {
            when {
                expression {
                    BRANCH_NAME == 'dev' /*&& CODE_CHANGES == true*/
                }
            }
            steps {
                echo 'building the application...'
                echo "building commit ${GIT_COMMIT}"
            }
        }
        
        stage("test") {
            when {
                expression {
                    BRANCH_NAME == 'dev' || BRANCH_NAME == 'master'
                }
            }
            steps {
                echo 'testing the application...'
                echo "testing version ${NEW_VERSION}"
            }
        }
        
        stage("deploy") {
            steps {
                script {
                    withCredentials([
                        usernamePassword( credentialsId: 'my-server-credentials', usernameVariable: 'username', passwordVariable: 'password')
                    ])
                    {
                        print 'using credentials: '
                        print 'username=' + username + ', password=' +password
                        print 'username.collect { it }='+username.collect { it }
                        print 'password.collect { it }='+password.collect { it }
                    }
                }
                echo 'deplying the application...'

            }  
        }
    } 

    post {
        success{
            echo 'The pipeline was successfully run !'
        }

    }
}
