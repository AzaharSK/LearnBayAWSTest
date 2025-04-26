
![Screenshot from 2025-04-26 10-10-44](https://github.com/user-attachments/assets/f016b3eb-71e2-40cb-8931-256dfd13dcb5)


# Question 7: create a python lamda function on aws console to stop EC2 instance if it was running in aws lamda code editor


![2025-04-26_10-41](https://github.com/user-attachments/assets/aabd93dc-62af-411d-a0d1-b9cb79769304)

```python
import json
import boto3

# Initialize a session using Amazon EC2
ec2 = boto3.client('ec2')
 
def stop_all_running_instances():
    try:
        # Describe instances and filter only running instances
        response = ec2.describe_instances(
            Filters=[{'Name': 'instance-state-name', 'Values': ['running']}]
        )

        # Extract all instance IDs of running instances
        instance_ids = []
        for reservation in response['Reservations']:
            for instance in reservation['Instances']:
                instance_ids.append(instance['InstanceId'])

        # Check if there are any running instances
        if instance_ids:
            print(f"Found the following running instances: {instance_ids}")
            # Stop the running instances
            stop_response = ec2.stop_instances(InstanceIds=instance_ids)
            print(f"Stopping instances: {stop_response}")
        else:
            print("No running instances found.")

    except Exception as e:
        print(f"An error occurred: {e}")

# Run the function to stop all running instances
stop_all_running_instances()

```

![2025-04-26_10-45](https://github.com/user-attachments/assets/2ce86b21-ff74-42cc-a666-d64556e74269)

![2025-04-26_10-48](https://github.com/user-attachments/assets/c83ba02c-b53b-494c-a4dc-35ab1e7f2d19)


