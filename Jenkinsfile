pipeline {
    agent: any

    stages {
        // There should be a "check out" stage. But since we are using SCM, we don't need to do this stage.

        stage('Build') {
            steps {
                //clean
                sh '"./mvnw" clean'

                // Maven install dependencies

                sh '"./mvnw" install'
                // Maven build
                sh '"./mvnw" spring-boot:run'
            }
        }

    }
}