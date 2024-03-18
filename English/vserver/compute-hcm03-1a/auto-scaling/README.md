# Auto Scaling

Auto-scaling is a service that automatically increases or decreases (scale) the server (VM) according to the conditions set by the user. Auto-scaling ensures high system availability while optimizing costs

### **Components of Autoscaling:** <a href="#autoscaling-componentsofautoscaling" id="autoscaling-componentsofautoscaling"></a>

**Profile**: Is a sample configuration setting of the instance including Flavor, Volume, Secure group, network. Auto scaling group will be based on the profile settings to scale Intance with the corresponding configuration.

Each profile can be attached to multiple scaling groups, however each scaling group can only be attached to a single profile.

Profile template configuration after successful creation cannot be edited. If there is a need to change, you will need to create a new profile.

**Auto Scaling group:** An auto scaling group will consist of multiple instances with the same configuration type defined in the profile. So each auto scaling group needs to be associated with 1 profile and there can't be more than 1 profile per group.

Auto scaling group will create the number of instances corresponding to the "desired capacity" setting and maintain this number even if 1 instance fails (un-healthy). The "healthy check" & "Recover node" features will check, terminate the failed instances and create a new instance, keeping the number of instances always guaranteed.

**Schedule:** This component will determine when auto-scale will execute, There are 3 ways to set it up:

* Manual: By changing the "desired capacity" at the Auto scaling group configuration interface, the number of instances will increase/decrease depending on the needs.
* Scheduler: set up a schedule to run automatically depending on needs. For example, setting a schedule to increase the number of instances during peak hours and setting a schedule to reduce the number of instances during off-peak hours to optimize costs.
* Receiver: Allows you to scale (In/out) an auto-scaling group via http url. Webhook receivers are often used when you have a monitor tool available.

**Policy:** When attached to an auto-scaling group, the policy defines how to scale the group. Policy includes two types:

* Load ballancer policy: This policy helps instances created by auto-scaling automatically be added to the Load ballancer pool.
* Scaling policy: This policy will define the following properties: Scaling out, scaling in, how many instances each time increases / decreases, the cooldown between each scale

A policy can be attached to many different auto-scaling groups (except load balancer policies), saving you time when you have multiple auto scaling groups. Each auto-scaling group can attach more than 1 policy, but cannot attach the same policy type (for example, each group can only have 1 scaling out or 1 scaling in policy).
