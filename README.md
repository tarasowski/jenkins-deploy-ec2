# Jenkins Pipeline Deployment

## Overview
This Jenkins pipeline automates the deployment of a Node.js application to an EC2 instance. It consists of two primary stages:
1. **Clone Repository**: Pulls the latest code from the specified GitHub repository.
2. **Deploy to EC2**: Transfers the application files to the designated EC2 instance.

## Prerequisites
Before running this pipeline, ensure the following prerequisites are met:
- Jenkins is installed and configured.
- The Jenkins server has the necessary SSH credentials configured.
- The target EC2 instance is accessible from the Jenkins server.
- The Git repository contains the necessary deployment files.

## Pipeline Configuration

### Environment Variables
The following environment variables are used in the pipeline:

| Variable         | Description                                     | Default Value |
|-----------------|-------------------------------------------------|---------------|
| `EC2_USER`      | The SSH user for the EC2 instance              | `ubuntu`      |
| `EC2_HOST`      | The public IP address of the EC2 instance      | `54.234.21.215` (Change this) |
| `DEPLOY_PATH`   | The target directory on the EC2 instance       | `/home/ubuntu/app` (Change if needed) |
| `SSH_CREDENTIALS` | The Jenkins SSH credentials ID for authentication | `jenkins-ec2-key` |

### Pipeline Stages
#### 1. Clone Repository
This stage clones the application repository from GitHub. Update the repository URL if deploying a different project.

#### 2. Deploy to EC2
- Uses `sshagent` to establish a secure connection to the EC2 instance.
- Creates the target directory (`DEPLOY_PATH`) if it does not exist.
- Transfers all application files to the EC2 instance via `scp`.

## Setup Instructions

1. **Update Jenkins Credentials**
   - Go to Jenkins -> Manage Jenkins -> Manage Credentials.
   - Add a new SSH credential with the ID `jenkins-ec2-key` (or modify the pipeline to match an existing credential ID).

2. **Modify the Pipeline Script**
   - Change `EC2_HOST` to match your EC2 instance's public IP.
   - Update the GitHub repository URL in the `Clone Repository` stage.
   - Modify `DEPLOY_PATH` if necessary.

3. **Run the Pipeline**
   - Save the pipeline script in Jenkins.
   - Trigger a build to deploy the application.

## Troubleshooting
- **Connection Issues**: Ensure Jenkins can connect to the EC2 instance using SSH.
- **Permission Errors**: Check file and directory permissions on the EC2 instance.
- **Repository Not Found**: Verify the GitHub repository URL and branch.

## Future Enhancements
- Add a build step for installing dependencies.
- Implement automated testing before deployment.
- Use a CI/CD approach for better deployment management.

## License
This project is open-source and can be modified as needed.
