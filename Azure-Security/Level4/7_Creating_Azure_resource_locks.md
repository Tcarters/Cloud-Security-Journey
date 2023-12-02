# Creating Azure resource locks

__What are Azure resource locks?__

- Azure resource locks prevent users in an organization to accidently deleting or modifying critical resources.
- Azure locks are different from role-based access control in a way that using these locks you can apply restrictions across all users and roles.
- Users can apply locks on resource level, resource group level or subscription level.

There are two types of locks available in Azure:
* CanNotDelete: If this lock is applied to any of the resources, the user can still read or modify the resource but cannot delete it.
* ReadOnly: As the name suggests, with this lock applied, a user can only read the resource without causing any modifications or deletions.
* In the Azure portal, these locks are called Delete and Read-only.

## Architecture Diagram

![image](https://github.com/Tcarters/Cloud-Security-Journey/assets/71230412/a1f39e0b-0b28-4c54-a65d-7e818039bd0a)


### Task 2: Deploying a Virtual Machine

- A Ubuntu vm 20.04
  
![image](https://github.com/Tcarters/Cloud-Security-Journey/assets/71230412/13cbb41b-b41d-435a-b92a-2518d552de1a)


### Task 3: Creating a Delete Lock
- Click on the Virtual Machine you just created, and in the left panel click on Locks and then click Add.

- Delete Lock:
  
![image](https://github.com/Tcarters/Cloud-Security-Journey/assets/71230412/6fd179d1-4fe8-46eb-8b55-50c704da7359)

- Unable to delete Vm

![image](https://github.com/Tcarters/Cloud-Security-Journey/assets/71230412/ee741aba-49d9-4dca-9401-6af2b837a332)


### Task 4: Creating a Read-Only Lock

- Same with type ReadOnly Lock for Resource Group:

![image](https://github.com/Tcarters/Cloud-Security-Journey/assets/71230412/b750ab3d-aa38-41ad-b662-3f9e386eff40)

DOne.

