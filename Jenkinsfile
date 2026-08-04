podTemplate(yaml: readTrusted('pod.yaml')) {
    node (POD_LABEL) {
        stage('checkout') {
            git branch: main, url: ''
        }
        stage('build') {
            container('jdk-21') {
                sh '''
                ./mvnw clean package
                '''
            }
        }
    }
}