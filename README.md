# Task 26: Basic Cloud Monitoring Alert Using AWS CloudWatch

## Project Overview

This project was completed as part of the Veda Technology Cloud Computing Internship.

The objective was to configure an AWS CloudWatch alarm that monitors EC2 CPU utilization and sends an email notification through Amazon Simple Notification Service (SNS) when the alarm enters the `In alarm` state.

## Objectives

- Understand the difference between monitoring and automated alerting.
- Monitor EC2 CPU utilization using Amazon CloudWatch.
- Configure a threshold-based metric alarm.
- Integrate CloudWatch with Amazon SNS for email notifications.
- Verify the alarm state, configuration, and notification delivery.

## Technologies Used

- Amazon EC2
- Amazon CloudWatch
- Amazon Simple Notification Service (SNS)
- Ubuntu Server
- AWS Management Console

## Architecture

EC2 Instance → CloudWatch CPU Metric → CloudWatch Alarm → Amazon SNS Topic → Email Notification

## EC2 Configuration

| Setting | Configuration |
|---|---|
| Instance name | `veda-task26-monitoring-vm` |
| Operating system | Ubuntu Server |
| Instance type | `t3.micro` |
| AWS Region | Asia Pacific (Mumbai), `ap-south-1` |
| Monitoring metric | `CPUUtilization` |
| Monitoring interval | Basic monitoring |

## CloudWatch Alarm Configuration

| Setting | Configuration |
|---|---|
| Alarm name | `veda-task26-high-cpu-alarm` |
| Metric namespace | `AWS/EC2` |
| Metric | `CPUUtilization` |
| Statistic | Average |
| Period | 5 minutes |
| Threshold type | Static |
| Comparison operator | Greater than (`>`) |
| Threshold | 70% |
| Datapoints to alarm | 1 out of 1 |
| Missing data treatment | Treat as missing |

The alarm evaluates the average CPU utilization over a five-minute period. It enters the `In alarm` state when the metric exceeds 70% for the configured evaluation period.

## SNS Email Notification

An SNS topic named `veda-task26-cpu-alerts` was created and configured as the notification destination for the CloudWatch alarm's `In alarm` state.

The email subscription was confirmed, and a manually published SNS test message was successfully received in the email inbox.

**Testing note:** The manually published SNS message verifies email delivery through SNS. It does not, by itself, prove that a CPU threshold breach triggered an email notification.

## Verification Results

- EC2 instance launched and reached the Running state.
- EC2 status checks passed.
- CloudWatch CPU utilization metrics were visible.
- CloudWatch alarm was created and reached the `OK` state.
- SNS notification action was enabled on the alarm.
- SNS email subscription was confirmed.
- Manually published SNS test message was received by email.

The alarm was verified in its normal `OK` state. A real CPU threshold breach and the resulting CloudWatch-triggered email were not confirmed during this test.

## Screenshots

The `screenshots/` directory contains the evidence collected during implementation.

1. `01_EC2_Launch_Configuration.png` — EC2 configuration.
2. `02_CPU_Metric_Before_Alarm.png` — CPU utilization metrics.
3. `03_CloudWatch_CPU_Metric_Selection.png` — Selected CloudWatch metric.
4. `04_CloudWatch_Threshold_Configuration.png` — Alarm threshold configuration.
5. `05_CloudWatch_SNS_Notification_Configuration.png` — SNS action configuration.
6. `06_SNS_Email_Subscription_Confirmed.png` — Confirmed email subscription.
7. `07_CloudWatch_Alarm_Created.png` — Created CloudWatch alarm.
8. `08_CloudWatch_Alarm_Details_Verification.png` — Alarm details.
9. `09_CloudWatch_Alarm_Actions.png` — Enabled notification action.
10. `10_CloudWatch_Alarm_History.png` — Alarm creation and state history.
11. `11_SNS_Test_Message_Published.png` — SNS test publication.
12. `12_SNS_Email_Received.png` — Received test email.

## Key Learnings

- CloudWatch collects metrics that help monitor AWS resources.
- Alarms evaluate metric values against configured thresholds.
- SNS can distribute notifications to subscribed email endpoints.
- Alarm state history helps verify configuration and state transitions.
- Monitoring and alerting are different: monitoring observes metrics, while alerting notifies users when configured conditions are met.

## Cost and Cleanup

AWS usage may incur charges depending on account eligibility, resource configuration, and usage.

After collecting the required evidence, review the resources created for this task. Stop or terminate the EC2 instance when it is no longer needed, and remove temporary resources when appropriate. Remember that stopped instances can still incur storage charges, and CloudWatch alarms and other resources may have associated costs.

