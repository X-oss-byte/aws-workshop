---
title: "Cleanup"
chapter: true
weight: 1
---

# Cleanup

Since every resource in this workshop was deployed using CloudFormation, cleaning up the workspace involving just deleting the stack:
To delete a stack, open the AWS CloudFormation console at https://console.aws.amazon.com/cloudformation.

Then, On the Stacks page in the CloudFormation console, select the stack that you want to delete and - in the stack details pane - choose Delete.

In addition, when prompted, select Delete again.

{{% notice tip %}}
The stack deletion operation can't be stopped once the stack deletion has begun. The stack proceeds to the `DELETE_IN_PROGRESS` state.
{{% /notice %}}

After the stack deletion is complete, the stack will be in the `DELETE_COMPLETE` state. Stacks in the `DELETE_COMPLETE` state aren't displayed in the CloudFormation console by default. To display deleted stacks, you must change the stack view filter as described in Viewing deleted stacks on the AWS CloudFormation console.

If the delete failed, the stack will be in the `DELETE_FAILED` state. For solutions, see the [Delete stack fails troubleshooting topic](https://docs.aws.amazon.com/AWSCloudFormation/latest/UserGuide/troubleshooting.html#troubleshooting-errors-delete-stack-fails).