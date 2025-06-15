### Create an EKS cluster; Steps Overview

* IAM role for EKS service - gives the service permissions in the account

* Create a VPC where the worker nodes will run

* Create EKS cluster - a set of control plane nodes managed by aws

* Connect to the EKS cluster from local machine using kubectl

* create a IAM role for the group of worker nodes

* Create the node group (a group of worker nodes) that will run inside the VPC and be attached to the EKS cluster (control plane nodes)

* Configure auto-scaling for the cluster 

* Deploy an app to the EKS cluster
_____________________________________________

### Detailed Steps

* IAM role for Node Group (worker nodes)

    - Ec2 service
      Attach policies: 
      * AmazonEKSWorkerNodePolicy
      * AmazonEC2ContainerRegistryReadOnly 
      * AmazonEKS_CNI_Policy 
      (Container Network Interface in K8s, allows the pods in the cluster to communicate with each other no matter where they are located)

      
* Add node group to EKS cluster

    - EKS -> compute -> configure node group
      instance type: t3.small
      node group scaling configuration: set the desired, min and max size of the node group, depending on the workload.
      
      
* Configure auto-scaling

    $ kubectl apply -f https://raw.githubusercontent.com/kubernetes/autoscaler/master/cluster-autoscaler/cloudprovider/aws/examples/cluster-autoscaler-autodiscover.yaml

    $ kubectl get deployment -n kube-system cluster-autoscaler
    #show the cluster autoscaler deployment component

    $ kubectl edit deployment -n kube-system cluster-autoscaler #edit the running autoscaler deployment

    