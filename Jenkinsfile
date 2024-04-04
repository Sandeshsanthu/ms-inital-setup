node {
    // def repourl = "${REGISTRY_URL}/${PROJECT_ID}/${ARTIFACT_REGISTRY}"
    // def mvnHome = tool name: 'maven', type: 'maven'
    // def mvnCMD = "${mvnHome}/bin/mvn"
    stage('Checkout') {
        checkout([$class: 'GitSCM',
         branches: [[name: '*/main']],
          extensions: [],
          userRemoteConfigs: [[url: 'https://github.com/Sandeshsanthu/ms-inital-setup.git']]
        ])
    }
    // stage('Build and Push') {
    //     withCredentials([file(credentialsId: 'gcp', variable: 'GC_KEY')]) {
    //         sh("gcloud auth activate-service-account --key-file=${GC_KEY}")
    //         sh 'gcloud auth configure-docker us-central1-docker.pkg.dev'
    //         sh "${mvnCMD} clean install jib:build -DREPO_URL=${REGISTRY_URL}/${PROJECT_ID}/${ARTIFACT_REGISTRY}"
    //     }
    // }
    // stage('Debug') {
    //     // Print the content of the deployment.yaml file
    //     sh "cat k8s/deployment.yaml"
    // }
    stage('Deploy') {
        // sh "sed -i 's|IMAGE_URL|${repourl}|g' k8s/deployment.yaml"

        step([$class: 'KubernetesEngineBuilder',
             projectId: env.PROJECT_ID,
             clusterName: env.CLUSTER,
             location: env.ZONE,
             manifestPattern: 'k8s/',
             credentialsId: 'GCP',
             verifyDeployments: true 
            ])
    }
}
