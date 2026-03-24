# Lab M6.02 - Create Basic Threshold Alert

## Overview
In this lab, I configured basic monitoring and alerting using Amazon CloudWatch. The goal was to detect when system resources reach critical levels and notify the user automatically.

To achieve this, I created CloudWatch alarms based on CPU, memory, and disk usage metrics, and connected them to an SNS topic that sends email notifications when thresholds are exceeded.

## Alarms Created

| Alarm Name | Metric | Threshold | Evaluation Period |
|------------|--------|----------|-------------------|
| HighCPUUtilization | CPUUtilization | 80% | 2 × 5 min |
| HighMemoryUtilization | MemoryUtilization | 85% | 2 × 5 min |
| LowDiskSpace | disk_used_percent | 80% | 1 × 5 min |

## Threshold Rationale

The thresholds were chosen based on common operational practices:

- CPU (80%): Indicates sustained high load without reacting to short spikes.
- Memory (85%): Leaves some buffer before performance degradation.
- Disk (80%): Prevents running out of space before it impacts the system.

## Testing

To verify the alarms, I generated CPU load using the stress tool on the EC2 instance.

Steps followed:
1. Installed the stress tool on the instance.
2. Ran a CPU stress test for 15 minutes.
3. Monitored the alarm state in CloudWatch.
4. Confirmed that the alarm transitioned from OK to ALARM.
5. Verified that an email notification was received via SNS.

## Screenshots

The following screenshots are included in this repository:

- SNS topic and confirmed email subscription  
- Alarm in OK state  
- Alarm in ALARM state after triggering  
- Email notification received  

## Challenges & Solutions

One issue encountered was that environment variables like INSTANCE_ID and TOPIC_ARN were not always available in new terminal sessions, which caused errors when creating alarms. This was resolved by redefining the variables before running the commands.

Another issue was not seeing the alarm in the AWS Console, which was solved by selecting the correct region (eu-central-1).

## Conclusion

This lab demonstrates how to implement basic monitoring and alerting in AWS using CloudWatch and SNS. With these alerts in place, it becomes possible to react quickly to system issues before they impact users.