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
        stage('image build') {
            container('buildkit') {
                sh """
                    ls -la
                    buildctl --addr tcp://buildkitd.devops-tools.svc.cluster.local:1234\
                    --tlscacert /certs/ca.pem\
                    --tlscert /certs/cert.pem\
                    --tlskey /certs/key.pem\
                    build --frontend dockerfile.v0\
                    --opt filename=Dockerfile --local context=.\
                    --local dockerfile=.\
                    --output type=image,name=134448505602.dkr.ecr.ap-south-1.amazonaws.com/retail-store-ui,push=true
                """
            }
        }
    }
}