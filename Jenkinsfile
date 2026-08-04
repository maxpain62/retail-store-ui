podTemplate(yaml: readTrusted('pod.yaml')) {
    node(POD_LABEL) {
        stage('Checkout') {
            git branch: 'main', url: 'https://github.com/maxpain62/retail-store-ui.git'
        }
        stage('build') {
            container('java-build') {
                sh '''
                ./mvnw clean package
                '''
            }
        }
    }
}