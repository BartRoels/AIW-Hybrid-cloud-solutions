HOL-4: Exercise 4: Arc-enable existing Azure Stack HCI Virtual Machines
==============
Overview
-----------
You have deployed some virtual machines on the Azure Stack HCI Cluster leveraging the Windows Admin Center, it is now time to Arc-enable those assets and look at the Azure Arc-enabled Server capabilities.

Contents
-----------
- [HOL-4: Exercise 4: Arc-enable existing Azure Stack HCI Virtual Machines](#hol-4-exercise-4-arc-enable-existing-azure-stack-hci-virtual-machines)
  - [Overview](#overview)
  - [Contents](#contents)
  - [Task 1: Prepare your Azure environment before onboarding your Azure Arc-enabled Virtual Machine.](#task-1-prepare-your-azure-environment-before-onboarding-your-azure-arc-enabled-virtual-machine)
    - [Create a Resource Group](#create-a-resource-group)
    - [Add a Policy to the newly created Resource Group](#add-a-policy-to-the-newly-created-resource-group)
  - [Task 2: Azure Arc-enable VM002 - Ubuntu Linux 22.04](#task-2-azure-arc-enable-vm002---ubuntu-linux-2204)
    - [Prepare the step in Azure to onboard VM002 as an Azure Arc-enabled Virtual Machine](#prepare-the-step-in-azure-to-onboard-vm002-as-an-azure-arc-enabled-virtual-machine)
    - [Azure Arc-enable virtual machine VM002](#azure-arc-enable-virtual-machine-vm002)
  - [Task 3: Leverage the Azure AD RBAC controls to securely connect to VM002 via the Azure Arc-enabled Server capabilities](#task-3-leverage-the-azure-ad-rbac-controls-to-securely-connect-to-vm002-via-the-azure-arc-enabled-server-capabilities)
  - [Prepare  the Azure Connected Machine agent confiruration on the VM002](#prepare--the-azure-connected-machine-agent-confiruration-on-the-vm002)
  - [Summary](#summary)
  - [Product improvements](#product-improvements)
  - [Raising issues](#raising-issues)


Task 1: Prepare your Azure environment before onboarding your Azure Arc-enabled Virtual Machine.
-----------
In this step, you will create a new Azure Resource Group and assign an extra Azure Policy to this Resource Group.

### Create a Resource Group ###

1. In the "Search resources, services, and docs" search box at the top of the Azure Portal page, type **Resource Group** and click **Resource Groups** under Services.

    ![Create Azure Resource Group](./media/azrg-1.png "Create Azure Resource Group")
    
2. On the **Resource Groups** page, click **+ Create**.

    ![Create Azure Resource Group](./media/azrg-2.png "Create Azure Resource Group")

3. On the **Create a resource group** page, type **ArcServers-rg** in the **Resource Group** field. Click **Review + create**. On the next screen click **Create**, to create the new Resource Group.

    ![Create Azure Resource Group](./media/azrg-3.png "Create Azure Resource Group")

### Add a Policy to the newly created Resource Group ###

1. On the **Resource Groups** page, click on the resource group **ArcServers-rg**.

    ![Create Azure Resource Group](./media/policy-1.png "Create Azure Resource Group")
    
2. On the **ArcServers-rg** page, under **Settings**, click **Policies**.

    ![Create Azure Resource Group](./media/policy-2.png "Create Azure Resource Group")

3. On the **Policy | Compliance** page, click **Assign Policy**.

    ![Create Azure Resource Group](./media/policy-3.png "Create Azure Resource Group")

4. On the **Assign policy** page, click on the 3 dots on the right of the **Policy definition** field. On the **Available Definitions** page, type in the search field **Configure periodic checking for missing system updates on Azure Arc-enabled servers**. select the policy found below under the Policy Name, **[Preview]: Configure periodic checking for missing system updates on Azure Arc-enabled servers**. Click **Add**.

    ![Create Azure Resource Group](./media/policy-4.png "Create Azure Resource Group")

5. On the **Assign policy** page, click **Remediation**. Mark the checkbox before **Create a remediation task**.

    ![Create Azure Resource Group](./media/policy-5.png "Create Azure Resource Group")

6. On the **Assign policy** page, click **Review + create**. Click **Create**.

    ![Create Azure Resource Group](./media/policy-6.png "Create Azure Resource Group")

7. After a couple of minutes you should see an extra Policy assignment popping up in the list of Assigned Policies.

    ![Create Azure Resource Group](./media/policy-7.png "Create Azure Resource Group")


Task 2: Azure Arc-enable VM002 - Ubuntu Linux 22.04
-----------
In this step, you will download a Windows Server 2022 and Ubuntu Server 22.04 .Iso file and upload the .Iso to your Clustered Shared Volume you explored in Task 1. 

### Prepare the step in Azure to onboard VM002 as an Azure Arc-enabled Virtual Machine ###

1. In the "Search resources, services, and docs" search box at the top of the Azure Portal page, type **Machines - Azure Arc** and click **Machines - Azure Arc** under Services.

    ![Create Azure Resource Group](../media/hyd41.png "Create Azure Resource Group")
    
2. On the **Azure Arc | Machines** page, Click on **+ Add a machine**.

    ![Create Azure Resource Group](../media/hyd42.png "Create Azure Resource Group")

3. On the **Add servers with Azure Arc** page, in the **Add a single server** box, Click on **Generate script**

    ![Create Azure Resource Group](./media/vm002arc-3.png "Create Azure Resource Group")

4. On the **Add a server with Azure Arc** page, on the *Prerequisites* tab., Click **Next**.

    ![Create Azure Resource Group](./media/vm002arc-4.png "Create Azure Resource Group")

5. On the **Add servers with Azure Arc** page, on the *Resource details* tab, select the Resource Group **ArcServers-rg**, select **Linux** as Operating System and then Click **Next**.

    ![Create Azure Resource Group](./media/vm002arc-5.png "Create Azure Resource Group")

6. On the **Add servers with Azure Arc** page, on the *Tags* tab, Click **Next**.
   > **NOTE**: If you want, you can, of course, add a Cutsom tag, but the best practice is that you do this via Azure Policies.

    ![Create Azure Resource Group](./media/vm002arc-6.png "Create Azure Resource Group")

7. On the **Add a server with Azure Arc** page, on the *Download and run script* tab, Click **Download** (You later can find it in your Downloads folder). Click **Close**.
   
    ![Create Azure Resource Group](./media/vm002arc-7.png "Create Azure Resource Group")

### Azure Arc-enable virtual machine VM002 ###
 
1. On **AdminCenter** VM,  type **Cmd** in the searchbox (right from Start) and then **Enter**. Right-click the Command Prompt, and click **Run as administrator**.
 
    ![](./media/vm002arc-8.png "")

2. When receiving a **User Account Control** popup screen Click **Yes**
 
    ![](./media/vm002arc-9.png "")

3. In the **Command Prompt** window, type **scp "C:\Users\arcdemo\Downloads\OnboardingScript.sh" arcdemo@192.168.200.211:OnboardingScript.sh** and **Enter**. Type the Password ***ArcPassword123!!*** and **Enter**. By doing this we will copy the Azure Arc-enabled Server Onboarding Script **OnboardingScript.sh** to VM002.

    > **``NOTE``** Make sure to change the IP address according to your environment!
 
    ![](./media/vm002arc-10.png "")

4. In the **Command Prompt** window, type **ssh arcdemo@192.168.200.211** and **Enter*. Type the Password ***ArcPassword123!!*** and **Enter**. You now SSHed into the VM002 Virtual Machine.

    > **NOTE**: Make sure to change the IP address according to your environment!
 
    ![](./media/vm002arc-11.png "")

5. In the **Command Prompt** window, type **ls** and **Enter**. You now should see the uploaded Azure Arc-enabled Server Onboarding script **OnboardingScript.sh**. Next start the Onboarding Script by typing **bash ~/OnboardingScript.sh** and **Enter**. If asked provide the Password **ArcPassword123!!** and **Enter**.
 
    ![](./media/vm002arc-12.png "")

6. When you receive the below screen, double-click on the code and then click on your right mouse button to put the code on your Clipboard.
 
    ![](./media/vm002arc-13.png "")

7. Open a new browser tab and go to **https://aka.ms/devicelogin**, paste the Code from your Clipboard (check if there is no extra space behind the code!). Click **Next**.
 
    ![](./media/vm002arc-14.png "")

8. Click on the Username. Click **Ask later**. Click **Continue**. Close the Browser tab.
 
    ![](./media/vm002arc-15.png "")
    ![](./media/vm002arc-16.png "")
    ![](./media/vm002arc-17.png "")

9.  Go back to the **Command Prompt** window, where you should see something similar to the below screenshot. Type **exit** and **Enter** to disconnect the SSH connection. Type **Exit** again to close the Command Prompt.
 
    ![](./media/vm002arc-18.png "")

10. In the "Search resources, services, and docs" search box at the top of the Azure Portal page, type **Machines** and click **Machines - Azure Arc** under Services.

    ![](../media/hyd41.png "")

11. On the **Azure Arc | Machines** page, Click on **vm002**, which you just added as an Azure Arc-enabled virtual machine to Azure.

    ![](./media/vm002arc-19.png "")

12. On the **vm002** page, click **Policies** under Operations.
    
    Do you remember that you assigned an Azure Policy to the Resource Group **ArcServers-rg** at the beginning of this exercise? 
    Now you can check if this Azure policy was successfully assigned to VM002 we added to that Resource Group.

    ![](./media/vm002arc-20.png "")

13. As you will notice the policy was successfully assigned. This is just an example of the power of using Azure Policies. Imagine what you all can automate just by leveraging Azure Policies, not only for Compliance, regulations, Privacy, ... checks

    > **NOTE**: This can take a while, so if the "Compliance state" column is stating "Not Started", grab a coffee and check again later (+- 5 minutes).
        
    ![](./media/vm002arc-21.png "")


Task 3: Leverage the Azure AD RBAC controls to securely connect to VM002 via the Azure Arc-enabled Server capabilities
----- 
In this step, you will prepare the Azure Connected Machine agent on the VM002 to securely connect to VM002

## Prepare  the Azure Connected Machine agent configuration on the VM002 ##

1. On **AdminCenter** VM,  type **Cmd** in the searchbox (right from Start) and then **Enter**. Right-click the Command Prompt, and click **Run as administrator**.
 
    ![](./media/vm002arc-8.png "")

2. When receiving a **User Account Control** popup screen Click **Yes**.
 
    ![](./media/vm002arc-9.png "")

3. In the **Command Prompt** window, type **ssh arcdemo@192.168.200.211** and **Enter**. Type the Password **ArcPassword123!!** and **Enter**. You now SSHed into the VM002 Virtual Machine.
 
    ![](./media/vm002arc-11.png "")

4. In the **Command Prompt** window, type **sudo -i** and **Enter**. Type the Password **ArcPassword123!!** and **Enter**.
 
    ![](./media/ssh-1.png "")

5. In the **Command Prompt** window, type **azcmagent config list** and **Enter**. You will notice the configuration of the incomingconnections.ports value is empty

    ![](./media/ssh-2.png "")

6. In the **Command Prompt** window, type **azcmagent config set incomingconnections.ports 22** and **Enter**. Now type **azcmagent config list** and **Enter**. You will notice that the configuration of the incomingconnections.ports value is now set to **22**. Type **Exit** + **Enter** 3 times to close the Command Prompt.

    ![](./media/ssh-3.png "")

7. Go back to the Azure Portal and in the **"Search resources, services, and docs"** search box at the top of the Azure Portal page, type **vm002** and click **vm002** under **Resources**.

    ![](./media/ssh-4.png "")

8. On the **vm002** pagem click **Connect** under **settings**. On the **vm002 | Connect** page, click Password. Add **arcdemo** in the Username field. Click **Connect in browser**. If this is the first time you opened an Azure Shell, you will be asked to create a storage account. Click on **Create storage**.

    ![](./media/ssh-5.png "")

9. If all went well you should have established an SSH connection from within the Azure Portal to your on-premises Azure Arc-enabled Virtual Machine, for example on an Azure Stack HCI.

    > **``NOTE``** Learn more : https://learn.microsoft.com/en-us/azure/azure-arc/servers/ssh-arc-overview    

    ![](./media/ssh-6.png "")

    
Summary
-----------
In this exercise, you have been preparing and onboarding an on-premises Virtual Machine into the Azure control plane, leveraging the Azure Arc-enabled Server solution. We combined this onboarding with a quick look at what the power of Azure Policies can bring to you.
You finished this exercise by setting up and testing the new SSH access to Azure Arc-enabled servers.

With this completed, you can now move on to the next exercise.

Product improvements
-----------
If, while you work through this guide, you have an idea to make the product better, whether it's something in Azure Stack HCI, AKS on Azure Stack HCI, Windows Admin Center, or the Azure Arc integration and experience, let us know! We want to hear from you!

For **Azure Stack HCI**, [Head on over to the Azure Stack HCI Q&A forum](https://learn.microsoft.com/en-us/answers/tags/6/azure-stack-hci "Azure Stack HCI Q&A"), where you can share your thoughts and ideas about making the technologies better and raise an issue if you're having trouble with the technology.

For **AKS on Azure Stack HCI**, [Head on over to our AKS on Azure Stack HCI GitHub page](https://github.com/Azure/aks-hci/issues "AKS on Azure Stack HCI GitHub"), where you can share your thoughts and ideas about making the technologies better. If however, you have an issue that you'd like some help with, read on... 

Raising issues
-----------
This lab is based on the Azure Arc Jumpstart HCIBox: https://azurearcjumpstart.io/azure_jumpstart_hcibox/

If you want to set up the lab within your own Azure subscription please follow this link: https://azurearcjumpstart.io/azure_jumpstart_hcibox/#deployment-options-and-automation-flow

If you notice something is wrong with this guide, such as a step isn't working, or something just doesn't make sense - help us to make this guide better!
