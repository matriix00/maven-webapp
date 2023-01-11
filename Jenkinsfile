node{
    
    stage('Clone repo'){
        git credentialsId: 'GIT-Credentials', url: 'https://github.com/matriix00/maven-webapp.git'
    }
    
    stage('Maven Build'){
        def mavenHome = tool name: "maven", type: "maven"
        def mavenCMD = "${mavenHome}/bin/mvn"
        sh "${mavenCMD} clean package"
    }
    
//     stage('SonarQube analysis') {       
//         withSonarQubeEnv('sonar-app') {
//         def mavenHome = tool name: "maven", type: "maven"
//         def mavenCMD = "${mavenHome}/bin/mvn"
//        	sh "${mavenCMD} sonar:sonar"    	
//     }
// }
        
    stage('upload war to nexus'){
		nexusArtifactUploader artifacts: [	
			[
				artifactId: '01-maven-web-app',
				classifier: '',
				file: 'target/01-maven-web-app.war',
				type: "war",
			]	
		],
		credentialsId: 'nexus-secrets',
		groupId: 'in.ashokit',
		nexusUrl: '54.174.47.242:8081/',
		protocol: 'http',
		repository: 'simpleapp-release'
		version: '1.0.0'
	
}
    
//     stage('Build Image'){
//         sh 'docker build -t magdy79/mavenwebapp .'
//     }
    
//     stage('Push Image'){
//         withCredentials([string(credentialsId: 'dockerhub-secret', variable: 'pass')]) {
//             sh 'docker login -u magdy79 -p ${pass}'
//         }
//         sh 'docker push magdy79/mavenwebapp'
//     }
    
//     stage('Deploy App'){
//         kubernetesDeploy(
//             configs: 'maven-web-app-deploy.yml',
//             kubeconfigId: 'Kube-Config'
//         )
//     }    
//}
}
