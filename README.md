# Accuknox
Presentation: Kubernetes Security and Runtime Security Tools

Problem Statement 2: Local Kubernetes Cluster and DVWA Deployment
Step 1: Set Up a Local Kubernetes Cluster
We'll use Minikube for this example, but you can use any tool like k3s as well.

Install Minikube and kubectl
Install Minikube:
Follow the installation guide for Minikube from the official documentation: Minikube Installation.

Install kubectl:
Follow the installation guide for kubectl from the official documentation: kubectl Installation.

Start Minikube
bash
Copy code
minikube start --memory=4096 --cpus=2
Step 2: Deploy the DVWA Application
Create Kubernetes Manifests
Create a directory for your project and navigate into it:

bash
Copy code
mkdir dvwa-k8s
cd dvwa-k8s
Create the following files:

Deployment Manifest (deployment.yaml):
yaml
Copy code
apiVersion: apps/v1
kind: Deployment
metadata:
  name: dvwa
spec:
  replicas: 1
  selector:
    matchLabels:
      app: dvwa
  template:
    metadata:
      labels:
        app: dvwa
    spec:
      containers:
      - name: dvwa
        image: vulnerables/web-dvwa
        ports:
        - containerPort: 80
Service Manifest (service.yaml):
yaml
Copy code
apiVersion: v1
kind: Service
metadata:
  name: dvwa
spec:
  type: NodePort
  selector:
    app: dvwa
  ports:
    - protocol: TCP
      port: 80
      targetPort: 80
      nodePort: 30001
Deploy DVWA on Kubernetes
Apply the manifests to deploy DVWA:

bash
Copy code
kubectl apply -f deployment.yaml
kubectl apply -f service.yaml
Access DVWA
Get the Minikube IP:

bash
Copy code
minikube ip
Access DVWA at http://<minikube-ip>:30001. You should see the DVWA login page.

Step 3: Showcase/Demo 3 Attack Surfaces
For the demonstration, we'll show three attack surfaces: SQL Injection, Cross-Site Scripting (XSS), and Command Injection.

1. SQL Injection
Navigate to the 'SQL Injection' page:
Log in with default credentials (admin/password). Go to Vulnerabilities -> SQL Injection.

Perform an SQL Injection:
Enter 1' OR '1'='1 in the User ID field and submit. This should display all user information.

Document the Process and Results:

Screenshot of the SQL Injection input and results.
Explanation of how the attack works and its impact.
2. Cross-Site Scripting (XSS)
Navigate to the 'XSS (Reflected)' page:
Go to Vulnerabilities -> XSS (Reflected).

Perform an XSS Attack:
Enter <script>alert('XSS')</script> in the input field and submit. An alert box should pop up.

Document the Process and Results:

Screenshot of the XSS input and alert box.
Explanation of how the attack works and its impact.
3. Command Injection
Navigate to the 'Command Injection' page:
Go to Vulnerabilities -> Command Injection.

Perform a Command Injection:
Enter 8.8.8.8 && ls in the IP address field and submit. This should list files in the web server directory.

Document the Process and Results:

Screenshot of the Command Injection input and results.
Explanation of how the attack works and its impact.
Conclusion and Cleanup
After completing the demonstrations, you can clean up the resources:

bash
Copy code
kubectl delete -f deployment.yaml
kubectl delete -f service.yaml
minikube stop
minikube delete
Expected Output
Sample Kubernetes Setup:

Provide the Kubernetes manifests (deployment.yaml, service.yaml).
Describe the steps to set up Minikube and deploy DVWA.
Demo/Execution of the Attack Vectors:

Screenshots or recordings of the attack execution.
Explanation of each attack surface and the results.
Possible mitigation strategies for each demonstrated attack (e.g., using parameterized queries for SQL Injection, input sanitization for XSS, and limiting command execution for Command Injection).
