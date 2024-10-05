# AWS Resource Management Script

This project contains Python scripts to automate the creation and deletion of AWS resources such as EC2 instances, load balancers, target groups, launch templates, and SNS notifications. The scripts utilize the `boto3` library to interact with AWS services, streamlining infrastructure management.

## Table of Contents

- [Prerequisites](#prerequisites)
- [Installation](#installation)
- [Project Structure](#project-structure)
- [Usage](#usage)
  - [Creating Resources](#creating-resources)
  - [Deleting Resources](#deleting-resources)
- [Configuration](#configuration)
- [Code Explanation](#code-explanation)
- [License](#license)

## Prerequisites

- An AWS account
- Python 3.6 or later
- AWS CLI configured with appropriate permissions
- Required Python packages

## Installation

1. **Clone the repository:**

   ```bash
   git clone https://github.com/devops-bharat05/Monitoring-Scaling-Automation01
   cd aws-resource-management
   ```

2. **Install required packages:**

   Use `pip` to install the required Python packages. You can create a `requirements.txt` file with the following content:

   ```plaintext
   boto3
   ```

   Then, run:

   ```bash
   pip install -r requirements.txt
   ```

3. **Set up AWS credentials:**

   Ensure you have your AWS credentials set up. You can do this by configuring the AWS CLI:

   ```bash
   aws configure
   ```

   Enter your `AWS Access Key`, `AWS Secret Key`, `region`, and `output format`.

## Project Structure

```
aws-resource-management/
├── config.py                # Configuration file for AWS resources
├── create_resources.py       # Script to create AWS resources
├── delete_resources.py       # Script to delete AWS resources
├── ec2instance.py           # Functions for EC2 instance management
├── filterEc2Tags.py         # Functions to filter EC2 instances by tags
├── launchtemplate.py         # Functions for creating and managing launch templates
├── loadbalancer.py           # Functions for creating and managing load balancers
├── sns_notification.py       # Functions for managing SNS notifications
├── target_grp.py             # Functions for creating and managing target groups
└── requirements.txt          # Required Python packages
```

## Usage

### Creating Resources

To create all the necessary AWS resources, run the `create_resources.py` script:

```bash
python create_resources.py
```

### Deleting Resources

To delete all the created AWS resources, run the `delete_resources.py` script:

```bash
python delete_resources.py
```

## Configuration

All configurable variables are located in `config.py`. You can modify these variables according to your requirements:

- `REGION_NAME`: AWS region where resources will be created.
- `KEY_PAIR`: Name of the key pair for EC2 instances.
- `SECURITY_GROUP_ID`: Security Group ID to associate with the EC2 instances.
- `SUBNET_IDS`: List of subnet IDs where the resources will be deployed.
- `AMI_ID`: Amazon Machine Image ID to use for the EC2 instances.
- `INSTANCE_TYPE`: Type of the EC2 instances to be created.
- `LAUNCH_TEMPLATE_NAME`: Name of the launch template.
- `AUTO_SCALING_GROUP_NAME`: Name of the auto-scaling group.
- `TARGET_GROUP_NAME`: Name of the target group for the load balancer.
- `INSTANCE_NAMES`: List of instance names for SNS notifications.

## Code Explanation

1. **`create_resources.py`**: This script orchestrates the creation of AWS resources in the following order:
   - Launch EC2 instances.
   - Create a target group for the load balancer.
   - Create a load balancer and attach listeners.
   - Create a launch template and an auto-scaling group.
   - Set up SNS notifications and CloudWatch alarms for monitoring.

2. **`delete_resources.py`**: This script handles the deletion of AWS resources in reverse order to avoid dependency issues:
   - Delete the auto-scaling group.
   - Delete the load balancer.
   - Delete the target group.
   - Terminate EC2 instances.

3. **Other Modules**:
   - **`ec2instance.py`**: Contains functions for managing EC2 instances, including launching and deleting instances.
   - **`filterEc2Tags.py`**: Provides utility functions to filter EC2 instances based on their tags.
   - **`launchtemplate.py`**: Manages the creation and deletion of launch templates.
   - **`loadbalancer.py`**: Contains functions for creating and managing load balancers.
   - **`sns_notification.py`**: Manages the creation of SNS topics and subscriptions, as well as setting up CloudWatch alarms.

## License

This project is licensed under the MIT License - see the [LICENSE](LICENSE) file for details.
```
