pipeline {

    // CODE_CHANGES = gitChangesQ();   // this will be a groovy script that will determine whether there were code changes or not 
                                       // in the code base we are building with this pipeline. It will return a boolean. We'll use 
                                       // this variable later, in the condition for the stages.  
    
    agent any
    
    stages {

        // custom environment variables for this pipeline
        environment {
            NEW_VERSION = '1.3.0'
        }

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
