# Elastic Container Service (ECS)
Amazon Elastic Container Service (Amazon ECS) is a fully managed container orchestration service that helps you easily deploy, manage, and scale containerized applications.

## Clusters
A cluster in ECS is a logical grouping of tasks or services. You can use clusters to isolate your applications. This way, they don't use the same underlying infrastructure.

### Creating a Cluster in ECS
To get started with ECS we create a cluster in the ECS console. We can do this by clicking on _Get started_ in the ECS console home, or by clicking on _Clusters_ on the left-hand side of the console. 

![](images/clusters.png)

We are then taken to the _Clusteers_ page of the console where we can view all of our ECS clusters. To create a cluster click on _Create cluster_, which will take you to the following page.

![](images/create-cluster.png)

Note that the _Default namespace_ will automatically change to the name you give the cluster, you can change this if you wish.

![](images/create-cluster-infra.png)

If we scroll down we can see that the cluster is automatically configured for AWS Fargate, which is a technology that we can use on ECS to run containers without having to manage servers or clusters of EC2 instances, hence why it is a __serverless__ offering.

Once we are happy with our configurations we click on _Create_ to create our cluster.

## Task definitions
In ECS a task definition is essentially a blueprint for for your application, in it you specify the various parameters of your application. For example, you can use it to specify parameters for the operating system, which containers to use, which ports to open for your application, and what data volumes to use with the containers in the task.

### Creating a Task definition
To create a task definition, click on _Task definitions_ on the left-hand side of your ECS console, there you can view all of your task definitions, to make a new one click on _Create new task definition_.

![](images/create-task-def.png)

We are then taken to this page, under _Task definition family_ the name should be an approprate one, for example, __Nginx__ if you are launching an Nginx server. You can then configure you containers, notice it asks for _Image URI_, if you have an image on DockerHub, you should be able to simply provide the _image:tag_ key-value pair, as you can see in the snippet above.

Once we're done with that, click _Next_, we will then be take to step 2 where we can configure environment, storage, etc.

![](images/create-td-config-env.png)

AWS Fargate is selected automatically as our app environment, but we can add EC2 instances if we wish. There are other sepcifications we can change such as OS, although you should select an OS that is compatible with your selected image. Once we are happy with our configurations we can review everything and then create our task definition.

### Deploy a Service or run a Task
When we create our task definition we will be notified imediately that our task definition has been successfully created and that we can deploy a service or run a task. To do this we head back to _Clusters_ in the ECS console and click on a cluster that we have created.

![](images/democluster.png)

_Task_ : The instantiation of a task definition within a cluster. After you create a task definition for your application within Amazon ECS, you can specify the number of tasks to run on your cluster.

_Service_ : You can use an Amazon ECS service to run and maintain your desired number of tasks simultaneously in an Amazon ECS cluster. How it works is that, if any of your tasks fail or stop for any reason, the Amazon ECS service scheduler launches another instance based on your task definition.

### Run a Task
I'll start off by running a task, we can do this by navigating to the cluster we wish to run the task on, or if we have just created a task definition we can click the _Deploy_ dropdown shown at the top of the above snippet, and we will be given the option to run a task. After clicking _Run new task_ we will be taken to the following page.

![](images/run-task.png)

We can select which custer we want our task to run on, since we only have one (_DemoCluster_) the window has already been completed. We can edit the _Compute configuration if we wish.

If we scroll down we can edit the deployment configuration, here we select the task definition we ceated earlier, in this case mine is _ApacheHTTPd_.

![](images/deploy-config.png)

For the purposes of this guide I've left everything else as their default. Once we've created the task we should see the following in our cluster under _Tasks_.

![](images/tasks.png)

To verify it works, we click on the task we just created to open it up, which should take us to the following page.

![](images/demotask.png)

Copy the _Public IP_ or click on _open address_, and what we should see is our container image via our browser.

![](images/ecs-http-browser.png)

### Deploy a Service
Now we are going to deploy a service in our cluster, to do this we select the cluster we want our service to run on, go to the _Services_ section and click _Create_. We will then be taken to a page that looks very similar to the one where we set up our task to run.

With deploying a service we are given additional options, such as attaching a Load Balancer, or to have Auto Scaling. For the purposes of this demo I will attach an Application Load Balancer to my service, we can use an existing ALB or create a new one. Once we're done we click _Create_ then we are taken back to our cluster, where after a couple of minutes we should see the following.

![](images/services.png)

As you can see you are notified that your deployment is in progress and that it may take a few minutes to be set up. You can view the progress in CloudFormation as well.

![](images/ecs-cloudformation.png)

As you can see in the above snippet, our service has been fully created with the resources we specified. And if we go back to our cluster in ECS we can see our service fully up and running.

![](images/deploy-success.png)

For more details we simply click on the service.

![](images/httpd-service.png)

Here we're provided with a variety of details on our services such as health, logs, configurations & tasks, etc. From what we can see under _Status_ we have two task running (which is the desired number that I set when creating the service), we can also see that the service has a load balancer attached (_ecs-alb_). For details on the tasks we can click on _Configuration and tasks_.

![](images/service-config.png)

The information here reflects what we specified when creating the service, for example, we wanted an application load balancer to be attached to our service. We can see under _Auto Scaling_ the desired number of tasks, but note there is no maximum or minimum number of tasks to be run because we didn't want auto scaling in this case. If we scroll down we will then be able to see the tasks associated with our service, and if we click on the task we can see the container running for that task.

![](images/service-tasks.png)

Note we can also see these tasks by navigating back to our cluster and selecting the _Tasks_ section. We can verify that our tasks are running properly in the same way as shown when launching a single task. Since we attached a load balancer to our servcie we want to verify that it works. So what we do is click on _ecs-alb_ which can be found under _Status_ in the _Health and metrics_ section of our service, this should take us to _Load Balancers_ in the EC2 console.

![](images/ecs-alb.png)

Then to verify it works, copy the _DNS name_ and then open a new tab in the browser and then search for it. 

![](images/ecs-alb-browser.png)

As we can see here our load balancer works!

Our service has 2 tasks running, suppose we stop one of these tasks, what will happen?

![](images/stop-task.png)

Here we have stopped a task, but our service has the deisred capacity set to 2, this means that if a task is stopped, either by us or due to health issues, a new task will automatically be created.

![](images/new-task.png)

This is done despite not having an Auto Scaling Group, if we wanted to change this we would have to update the service itself.

We can delete the service, and as a result all associated CloudFormation stacks and resources will be deletd as well.