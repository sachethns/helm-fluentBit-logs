# Helm Fluent Bit Logs

This repository contains a Helm chart for deploying Fluent Bit to Kubernetes clusters. The chart configures Fluent Bit to collect and forward logs from EKS control plane, container logs, and host logs to Amazon CloudWatch. It is designed to work seamlessly with Amazon EKS and AWS CloudWatch, providing robust log management and monitoring capabilities.

## Features

- **Multi-source Log Collection**: Collect logs from Kubernetes applications, systemd services, and host logs.
- **Centralized Logging**: Forward logs to Amazon CloudWatch for centralized monitoring and analysis.
- **Flexible Configuration**: Easily configure log collection and forwarding using Helm values.
- **JSON Log Format**: Ensure all logs, including Istio logs, are in JSON format for easy parsing and analysis.
- **Minimal Permissions**: Follows the principle of least privilege by using the appropriate AWS IAM roles and policies.

## Prerequisites

1. **Kubernetes Cluster**: A running Kubernetes cluster, preferably Amazon EKS.
2. **Helm**: Helm package manager installed and configured.
3. **AWS CLI**: AWS CLI configured with appropriate permissions.
4. **IAM Roles**: IAM roles with necessary permissions attached to the worker nodes.

## Installation

1. **Clone the Repository**

   ```sh
   git clone https://github.com/csye7125-su24-team17/helm-fluentBit-logs.git
   cd helm-fluentBit-logs
   ```
2. **Update values**  
   
   Edit the values.yaml file to configure your cluster-specific values:
   ```
   clusterName: "your-cluster-name"
   logsRegion: "your-region"
   httpServer: "On"
   httpPort: "2020"
   readFromHead: "Off"
   readFromTail: "On"
   ```
3. **Deploy the Chart**  
   
   Use Helm to deploy the chart to your Kubernetes cluster:  
   ```
   helm install fluent-bit ./helm-fluentBit-logs -n amazon-cloudwatch --create-namespace
   ```

## IAM Permissions

   Ensure that the worker nodes have the following IAM policy attached:

    
    CloudWatchAgentServerPolicy: Allows publishing logs to CloudWatch.
    

## Monitoring and Troubleshooting
   
   To monitor the status of the Fluent Bit pods, use:
   ```
   kubectl get pods -n amazon-cloudwatch
   ```
   To view logs from a specific Fluent Bit pod:
   ```
   kubectl logs <pod-name> -n amazon-cloudwatch
   ```

   For detailed debugging, check the CloudWatch logs in the AWS Management Console.

## Contributing  

We welcome contributions! Please fork the repository, make your changes, and open a pull request.

## Contact  

For questions or support, please open an issue on this GitHub repository.


