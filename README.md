# githubaction-code2
this project revolves around github where we have 2 git repos, one for the terraform code and the other for application code,
first we will start with terraform code workflow by using github actions we will create a workflow to apply any infra level change by using terraform this workflow is going to fetch the source code where we will have two branches one is stage and other is main, when we make any change to the stage branch the workflow will detect that and the terraform code will be tested through using terraform validate and plan to know the difference that is going to apply, when the staging branch is validated successfully this branch will be merged to the main branch through a pull request by the owner or authenticated user of main branch who can approve the changes to be applied against the infrastructure from the main branch.in the other repo we will have the app code, docker file and k8s definition files managed by helm. these are to apply any changes at app level, so we will have a workflow which will fetch, build,test and deploy the code. we will use maven with check style and sonar code analysis to test our code and validate it through quality gates, docker to build our docker image and upload it to Amazon ECR , after this helm charts which will be the bundle of k8s definition file which will be executed on EKS cluster

# steps to follow
- we will create IAM user, access keys, s3 bucket and ECR repo in AWS and will store it in github secrets

- now terraform code to setup vpc infra and eks cluster

- now time for github actions  to build and test our code by writting our workflow in our repo '.githib/workflows'

-  after this in the same workflow we will add steps to apply the terraform code only if there is change in main branch, we will add a step to execute terraform apply when we push to main branch

- in our workflow we will create nginx ingress controller for our application on k8s cluster, and also to execute kubectl command we will need kubeconfig file  

- now for second repo we will go first to test our code by using maven checkstyle and sonar analysis, build our docker image upload it to amazon ecr, build our helm charts which when we deploy it will 
  fetch the latest image from ecr and run the application 

- but first we will go to sonar cloud create our organization,project and token and store them in github secrets

- after this create our workflow create our sonar mention quality gate and mention mvn code checkstyle

- then we have to build our docker image and push it to our ECR

- build our helm charts from k8s definition files and pass the variables and its value of helm charts in the workflow , but we have first to mention our kubeconfig file to run our kubectl command and 
  storing aws credentials for our our eks cluster when fitshing the image from ecr so it has the auth.
