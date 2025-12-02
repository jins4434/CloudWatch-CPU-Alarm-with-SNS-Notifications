📘 CloudWatch CPU Alarm with SNS Email Notifications (AWS Project)
📌 Project Overview

This project demonstrates how to implement real-world AWS monitoring and alerting by creating a CloudWatch CPU Utilization Alarm for an EC2 instance and connecting it to Amazon SNS to send email notifications when CPU usage crosses a defined threshold.

A full hands-on PDF and screenshots are included in this repository.

🎯 Objectives

Create a CloudWatch alarm to monitor EC2 CPU Utilization

Configure an SNS topic for notifications

Subscribe an email address to SNS

Trigger the alarm intentionally using CPU stress

Validate email alert delivery

Document the full workflow

🏗️ Architecture Summary

EC2 Instance (Ubuntu)

Running and sending metrics to CloudWatch automatically

CloudWatch Metric

CPUUtilization (Average over 5 minutes)

CloudWatch Alarm

Threshold: >= 80% CPU

Period: 5 minutes

SNS Topic

Publishes notifications when alarm enters “ALARM” state

Email Subscription

Receives alert emails from SNS

🚀 Step-by-Step Implementation
1️⃣ Create an SNS Topic

Open AWS Console → SNS → Topics → Create topic

Type: Standard

Name: ec2-cpu-alerts

Click Create topic

2️⃣ Subscribe an Email to SNS

SNS → Topic → Your topic → Create subscription

Protocol: Email

Enter your email ID

Check inbox → Click the confirmation link

Status should change to Confirmed

3️⃣ Create a CloudWatch CPU Alarm

Go to CloudWatch → Alarms → Create alarm

Choose metric:
EC2 → Per-Instance Metrics → CPUUtilization

Select your instance ID

Configure:

Statistic: Average

Period: 5 minutes

Condition: >= 80%

Under Notification, select your SNS topic

Name your alarm → Create alarm

4️⃣ Trigger the Alarm (Testing)

SSH into your EC2 instance:

sudo apt update
sudo apt install -y stress
stress --cpu 2 --timeout 180


This will:

Push CPU above threshold

Trigger the CloudWatch alarm

SNS sends you an alert email

5️⃣ Verify Notification

You will receive an email from AWS Notifications showing:

Alarm Name

New State: ALARM

Threshold breach information
