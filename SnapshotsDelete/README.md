# AWS EBS Snapshot Cleanup

This project automates the process of deleting unused EBS snapshots in AWS, helping to manage costs and maintain a clean AWS environment.

## Overview

The solution uses AWS EventBridge to trigger a Lambda function daily, which identifies and deletes unattached EBS snapshots. It then sends a notification via Amazon SNS upon successful execution.

## Architecture

- AWS EventBridge: Schedules the daily run
- AWS Lambda: Executes the snapshot cleanup logic
- Amazon SNS: Sends email notifications

## Prerequisites

- AWS Account
- AWS CLI configured with appropriate permissions
- Python 3.8 or later

## Setup

1. Clone this repository:
2. Create an SNS topic for notifications.

3. Create a Lambda function:
- Runtime: Python 3.8+
- Handler: lambda_function.lambda_handler
- Environment variable: SNS_TOPIC_ARN (set to your SNS topic ARN)

4. Set up an EventBridge rule to trigger the Lambda function daily at 6 PM.

5. Configure IAM permissions for the Lambda function (see below).

## IAM Permissions

The Lambda function requires the following permissions:

- EC2:
- DescribeInstances
- DescribeVolumes
- DescribeSnapshots
- DeleteSnapshot
- CloudWatch Logs:
- CreateLogGroup
- CreateLogStream
- PutLogEvents
- SNS:
- Publish (to a specific SNS topic)

## Usage

The system runs automatically once set up. To manually trigger the Lambda function:

1. Go to the AWS Lambda console
2. Select your function
3. Click "Test" and create a test event (contents don't matter)
4. Click "Test" again to run the function

## Contributing

Contributions are welcome! Please feel free to submit a Pull Request.

## Acknowledgments

This project was inspired by the work of Abhishek Veeramalla. Special thanks to his YouTube channel for valuable insights on AWS cost optimization.
