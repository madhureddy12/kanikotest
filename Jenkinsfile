/**
 * This pipeline will build and deploy a Docker image with Kaniko
 * https://github.com/GoogleContainerTools/kaniko
 * without needing a Docker host
 *
 * You need to create a jenkins-docker-cfg secret with your docker config
 * as described in
 * https://kubernetes.io/docs/tasks/configure-pod-container/pull-image-private-registry/#create-a-secret-in-the-cluster-that-holds-your-authorization-token
 */

podTemplate(yaml: """
kind: Pod
spec:
  containers:
  - name: kaniko
    image: gcr.io/kaniko-project/executor:debug-539ddefcae3fd6b411a95982a830d987f4214251
    imagePullPolicy: Always
    command:
    - /busybox/cat
    tty: true
    
"""
  ) {

  node(POD_LABEL) {
    stage('Build with Kaniko') {
      git 'https://github.com/madhureddy12/kanikotest.git'
      container('kaniko') {
        sh '/kaniko/executor Dockerfile --insecure --skip-tls-verify --cache=true --destination=asia.gcr.io/gcp-shared-host-nonprod-260909/kaniko:latest'
      }
    }
  }
}
