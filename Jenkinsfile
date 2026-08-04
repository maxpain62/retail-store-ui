podTemplate(yaml: readTrusted('pod.yaml')) {
    node(POD_LABEL) {
        stage('Checkout') {
            git branch: 'main', url: 'https://github.com/maxpain62/retail-store-ui.git'
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