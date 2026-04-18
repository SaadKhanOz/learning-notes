CI/CD:
	 it is two steps:
	 1. continuous integration:
	 	integrating set of tools/process, that you follow before delivering your application to the customers.
	 2. continusous delivery:
	 	a process where you deploy your application or deliver your application on a specific platform to your customer.
	 	
	 for example:
	 	you develop the app and you are somewhere in the globe and there is customer which will see the app, so there should be a process which will reliably deliver this app to the customer:
	 	the process will test, scan for any security vulnerability, there shiuld be repostrs that suggest that app is perfect, finally u wil deploy ur app somewhere which your customer will be able to access.
	 	these stps might increase/decrease depending upon ur application that your are delivering to customer.
	 	
so cicd is the process that automate these steps.

Steps: (standard steps)
	unit test
	static code analysis
	code quality/ vulneability testing
	automation testing (end-to-end testing)
	repots
	deplying the application
	
Steps Explaination:
1. Unit Testing:
	testing the code with that specific functionality e,g add function in calculator application
	
2. static code analysis:
	for example, you have decleard 20 vars in code and uh have used 2 in them, that means you are wasting memory.
	so static analysis is testing code without running it, to look code is syntactically right, well formatted, didnot declare any unnecessary vars.
	
3. code quality/vulnerability analysis:
	testing if there is vulneability in the code
	
4. automation testing(functional testing/ end to end testing):
	u test the change u have done , does not impact other functiolaity, u verify ur app in end to end manner.
	
5. Reports:
	reposts are essentail that tellshow many code covergae is done, how much testing is passd, what is the code quality , is it fine or not. 
	
6. deployments:
	in this stage, you deplay ur app on a platform where ur cistomer can access it.
	
these stps can be done manually but will take time and there is a chance for error, instaed we will used cicd to do that.
we will be having stories in jira, we will make version of functionality and when we are sue about to deliver that, we can push to vcs (github, bitbucket, gitlab) and cicd will get hit and do these stps.

-------------------------------------

for example, we have a version1 and we have commited or pr to github, the cicd will take care of it.
so we will deploy jenkins in our org, this jenkin will look for commit/pr in out repo, if it is made, then jenkins will start set of actions.

jeckins will act as orchestrator, or act as pipe or tunnel, and start tools in it.

so devops engineer, will insatll these tools in jenkins, so whenever there is commit or pr to repo so these tools will get started.

thus, jenkins is orchestartor which will facilitate all of these tools.


wihout cicd, the app will be deleverd in months, thus, cicd is ensuring that app will be delevrd in minuted or hrs.

--------------------------------------
step1:
in jenkins terminology we call them pipelines,
so jenkins pipelines are something that take care of automating all of these tools and executing the actions that these tools do.

step2:
jenkins will also promote application to different stages.
to:
dev env , when confident so promote to 
staging env, and finally
to production environment

--------------------------------------
what are these stages:
usually, org divide thier environments to multiple env.
production env 0-> where customer are using ur app.
in some cases u will use preproduction env, and in somecases u will directly use the production env.
here ur cusotmer is using ur application.

there is difference between env to env, the production env will have alot of servers in it, it replicates the exact setup where u r deploying ur aplication to your customer.

staing env:
here, u might have less amount of cpu or ram and u wnat to deply ur app before evrytime u deply ur app to production.

dev env:
it is like -1 for ur staging.
the reson why ur app should be deployed to dev platform initially is because first u want to deply app n very simple env or simple ec2 insatnce or one k8s node (1 master and 1 worker node), once eberyti=hing is good in dev env, u can use manual or automatic approval where genkins shif app to staging env, 
in staging env, instaed of simple ec2 insatnce u might have cluster overhere, 3 master node and 5 worker node, when u test over there and everything is fine, then u use production env where u have 3 master and 30 worker nodes.

why not directly on production env? is becasue is is costly setup, first u want to check if app is working good with minimal setup and then uh can shift to complex setup (production env).

------------------------------------

jenkins is a platform or binary , u will insatll jenkins on one hist or ec2 instance/laptop, and then u keep adding machienes to it cz there are 100s of developer in org, and one jenkins node cannot take all the load.
so what u do, is to insatll jenkins master on one ec2 instance/laptop and then u keep connceting multiple ec2 insatnce to it.
so if u have 10 teams, uh say run the pipeline on node one for every change one repo, for team2 run it on node 2, and so on.
 
 ----------------------------------
  for scaleup the jenkins instances, uh have to have vms. for this uh need computes wich are costly.
  compute is ram, cpu and hardware.
  so, when u keep adding compute to jenkins insatnces, the steup becomes more costly and also the maintance become high.
  
 so uh have to make a setup which can scaleup and scaledown automatically, 
 
 one thing is, to integrate jenkins with auto scaling groups that can scaleup and down automatically, 
 but we are looking for realtime sceario, where uh want to scale down the jenkins to zero, like i dont want even a master node to exist, but this is not possible.
 
 like on weekends when there is no commit or code changes and zero pipelines to be executed, so incase of 20 microservise app, we have 20 jenkins setup means 20 master node and 3 worker nodes, so if u are not cinfiguring them well, so at any given time , u have 100s of vms that are not used but still running but my req is that when i am not making any changes to code, i dont want any server (0).
 in such cases, jenkns is not such a tool that uh should recommend or use.
 
 ---------------------------------
 eample of kubernetes :
 how kubernetes merge codes from developers throgh github and how it ensure that to not waste the vms.
 it uses shared resiurces, when ever there is commit or pr in repo, it creates k8s pods or docker containers and run the project, else the reosurces is used by another project.
 
 
 modern day cicd setup is github actions.
 no vms/resources wasted, resources consumed when there is pr or commit.
 
 
 
 
 
 
 
 
 
 
 
 
 
 
 
 
 
 
 
 
 
 
 
 
 
 
 
 
 
 
 
 
 
 
 


### **CI/CD Overview**

**CI/CD = Continuous Integration + Continuous Delivery (or Deployment)**

* **Continuous Integration (CI):**
  Developers frequently merge code into a shared repository. Each change is automatically **built, tested, and validated**.

* **Continuous Delivery (CD):**
  The application is automatically prepared for release. Deployment to production is usually a **manual approval step**.

* **Continuous Deployment (also CD):**
  Fully automated — every successful change is **automatically deployed to production** (no manual approval).

👉 So:

* CI = *build + test*
* CD = *release + deploy*

---

### **Why CI/CD?**

Without CI/CD:

* Releases take **weeks/months**
* Manual errors are common
* Integration becomes painful

With CI/CD:

* Faster delivery (minutes/hours)
* Automated quality checks
* Reliable deployments

---

### **Typical CI/CD Pipeline Stages**

1. **Build**
2. **Unit Testing**
3. **Static Code Analysis**
4. **Security / Vulnerability Scan**
5. **Integration / E2E Testing**
6. **Artifact Creation**
7. **Deployment**

---

### **Step-by-Step Explanation**

#### **1. Build**

* Convert source code → executable/package
* Example:

  * Java → `.jar`
  * Node.js → bundled app

---

#### **2. Unit Testing**

* Test individual components/functions
* Example:

```js
function add(a, b) {
  return a + b;
}
```

Test:

```js
expect(add(2,3)).toBe(5)
```

---

#### **3. Static Code Analysis**

* Analyze code **without running it**
* Detect:

  * Unused variables
  * Code smells
  * Bad practices

Tools:

* SonarQube
* ESLint

---

#### **4. Security / Vulnerability Testing**

* Check for:

  * SQL injection
  * Dependency vulnerabilities

Tools:

* Snyk
* OWASP scanners

---

#### **5. Integration / E2E Testing**

* Test entire application flow
* Example:
* Login → Dashboard → Payment

Tools:

* Selenium
* Cypress

---

#### **6. Reports**

* Show:

  * Code coverage
  * Test results
  * Quality metrics

---

#### **7. Deployment**

* Deploy app to:

  * Dev
  * Staging
  * Production

---

### **CI/CD Flow Example**

1. Developer pushes code to GitHub
2. Pipeline triggers automatically
3. Steps executed:

   * Build
   * Test
   * Scan
4. If all pass → deploy

---

## 🔧 Jenkins Explanation 

* **Jenkins = CI/CD tool + orchestrator**
* It does NOT "install tools inside it"
  → It **integrates with tools**

✔ Correct understanding:

* Jenkins runs pipelines
* Pipelines define steps
* Steps call tools (Maven, Docker, etc.)

---

### **Jenkins Pipeline**

* Defined using:

  * Jenkinsfile

Example:

```groovy
pipeline {
  stages {
    stage('Build') {
      steps {
        sh 'npm install'
      }
    }
    stage('Test') {
      steps {
        sh 'npm test'
      }
    }
  }
}
```

---

### **Jenkins Architecture **

* **Master (Controller):**

  * Manages pipelines

* **Agents (Workers):**

  * Execute jobs



* You **don’t need one Jenkins per microservice**
* One Jenkins can handle many projects

---

## 🌍 Environments 

### **1. Development Environment**

* Simple setup
* Used for initial testing

---

### **2. Staging Environment**

* Production-like
* Final testing before release

---

### **3. Production Environment**

* Real users
* High availability + scalability

---

### ❗ Why not deploy directly to production?

* Risky
* Expensive
* Bugs affect real users

---

## ⚡ Scaling Problem with Jenkins


### Problem:

* Jenkins requires:

  * Running servers (VMs)
  * Maintenance
* Even when idle → **cost still exists**

---

### Solution Approaches:

#### 1. Auto Scaling (Traditional)

* Use cloud VMs
* Scale agents up/down

---

#### 2. Kubernetes + Jenkins

* Run pipelines in **ephemeral pods**
* Pods created → run job → deleted

---

#### 3. Modern CI/CD (Best Practice)

### 👉 GitHub Actions

* Fully managed
* No infrastructure to manage
* Runs only when needed

✔ Benefits:

* Zero idle cost
* Easy setup
* Tight GitHub integration

---

## 🔥 Kubernetes in CI/CD 

Kubernetes **does NOT merge code**

Instead:

* CI/CD tool builds Docker image
* Pushes image to registry
* Kubernetes:

  * Pulls image
  * Deploys containers (pods)

---

### Example Flow:

1. Code pushed
2. CI builds Docker image
3. Image pushed to Docker Hub
4. Kubernetes deploys it

---

## 🧠 Important Concepts (Very Important for Interviews)

### 🔹 Artifact

* Output of build
* Example:

  * `.jar`, `.war`, Docker image

---

### 🔹 Pipeline as Code

* Define pipeline in code (Jenkinsfile, YAML)

---

### 🔹 Triggers

* Push
* Pull request
* Schedule

---

### 🔹 Rollback

* If deployment fails → revert to previous version

---

### 🔹 Blue-Green Deployment

* Two environments:

  * Blue (current)
  * Green (new)
* Switch traffic instantly

---

### 🔹 Canary Deployment

* Release to small % of users first

---



## 🚀 Final Simple Definition 

> CI/CD is an automated pipeline that builds, tests, and deploys applications, enabling faster and reliable software delivery.

---


