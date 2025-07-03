pipeline{
	
	agent any{

		stages{
			stage('Clone'){
				steps{
					git branch:'main',url:'https://github.com/dheerajn001/jenkins_project.git'
				}
			stage('Build'){
				steps{
					sh 'echo "Build th application..."'
				}
			}
			stage('Test'){
				steps{
					sh 'echo "Running tests.."'
				}
			}
			stage('Docker Build'){
				steps{
					sh 'docker build . -t --name flask-app:latest'
				}
			}
			stage('Docker Push'){
				steps{
					withCredentials([usernamePassword(credentialsId: 'dockerHub', usernameVeriable: 'USERNAME', passwordVeriable: 'PASSWORD')]){
					sh 'echo $PASSWORD |docker login -u $USERNAME --password-stdin'
					sh 'docker push $USERNAME/flask-app:latest'
					}
				}
			}
			stage('Deploy'){
				steps{
					script{
						sh 'docker stop flask || true'
						sh 'docker rm flask || true'
						sh 'docker run -d -p 5000:5000 --name flask $USERNAME/flask-app:latest'
					}
				}
			}
			
