def execute() {
    node() {
        String utils = load 'src/test/jenkins/lib/utils.jenkins'
        String revision = stage('Checkout') {
            checkout scm
            return utils.currentRevision()
        }
        gitlabBuilds(builds: ['build', 'test']) {
            stage('build') {
                gitlabCommitStatus('build') {
                    sh "echo  build "
                    sh "mvn clean package -DskipTests -DgitRevision=$revision"
                }
            }

            stage('test') {
                gitlabCommitStatus('test') {
                    sh "mvn verify -DgitRevision=$revision"
                }
            }
        }
    }
}

return this
