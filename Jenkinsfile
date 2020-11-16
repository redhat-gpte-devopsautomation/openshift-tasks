node {
  stage('Build Tasks') {
    openshift.withCluster() {
      openshift.withProject("bfb6-tasks") {
        openshift.selector("bc", "openshift-tasks").startBuild("--wait=true")
      }
    }
  }
  stage('Tag Image') {
    openshift.withCluster() {
      openshift.withProject("bfb6-tasks") {
        openshift.tag("openshift-tasks:latest", "openshift-tasks:${BUILD_NUMBER}")
      }
    }
  }
  stage('Deploy new image') {
    openshift.withCluster() {
      openshift.withProject("bfb6-tasks") {
        openshift.selector("dc", "openshift-tasks").rollout().latest();
      }
    }
  }
}
