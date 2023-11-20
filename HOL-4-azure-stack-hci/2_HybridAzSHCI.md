HOL-4: Exercise 2: Azure Stack HCI 22H2 Hybrid by design
==============
Overview
-----------
Discover, monitor, and manage the Azure Stack HCI hosts as well as the virtual machines. Extend your business to the cloud with an Azure hybrid solution. In this exercise, you can now begin to explore the Hybrid by-design capabilities of Azure Stack HCI 22H2 and Azure. We'll cover a few recommended activities below, to expose you to some of the key elements of Azure Stack HCI Hybrid by design capabilities.

Contents
-----------
- [HOL-4: Exercise 2: Azure Stack HCI 22H2 Hybrid by design](#hol-4-exercise-2-azure-stack-hci-22h2-hybrid-by-design)
  - [Overview](#overview)
  - [Contents](#contents)
  - [Task 1: Enable some Hybrid capabilities in Azure of your Azure Stack HCI cluster](#task-1-enable-some-hybrid-capabilities-in-azure-of-your-azure-stack-hci-cluster)
    - [Review the status of the Azure Arc required services in Windows Admin Center](#review-the-status-of-the-azure-arc-required-services-in-windows-admin-center)
  - [Task 2: Manage Azure Stack HCI clusters using Windows Admin Center in Azure](#task-2-manage-azure-stack-hci-clusters-using-windows-admin-center-in-azure)
    - [Enable all requirements so you can use Windows Admin Center in the Azure portal to manage a hybrid machine](#enable-all-requirements-so-you-can-use-windows-admin-center-in-the-azure-portal-to-manage-a-hybrid-machine)
  - [Task 3: Explore Azure Stack HCI Hybrid features in the Azure Portal](#task-3-explore-azure-stack-hci-hybrid-features-in-the-azure-portal)
    - [Explore Extensions](#explore-extensions)
    - [Configuration of The Azure Stack HCI 22H2 cluster in the Azure Portal](#configuration-of-the-azure-stack-hci-22h2-cluster-in-the-azure-portal)
  - [Summary](#summary)
  - [Product improvements](#product-improvements)
  - [Raising issues](#raising-issues)


Task 1: Enable some Hybrid capabilities in Azure of your Azure Stack HCI cluster
-----------
In this step, you will review the status of the Azure Arc services on the Azure Stack HCI 22H2 cluster by using Windows Admin Center, and enable Hybrid Azure Stack HCI Cluster features in the Azure Portal.

### Review the status of the Azure Arc required services in Windows Admin Center ###

1. Open **Windows Admin Center** on the **AdminCenter** VM. On the top left click on **All connections** and click on your previously deployed cluster, **hciboxcluster.jumpstart.local**

    ![Azure Arc WAC](./media/ReviewVolumes-1.png "Azure Arc WAC")
    
        
2. On the left-hand navigation, under **Configuration** select **Azure Arc**. For the central **Azure Arc** page, click **1. Azure Stack HCI registration**.

    ![Azure Arc WAC](./media/Arc-1.png "Azure Arc WAC")
    
3. On the **Azure Stack HCI registration** page, you should see ...
   
    ##### Azure Stack HCI system status: #####
   - **Connected** under the Azure connection status
   - **Registered** under the Azure Registration
    
    ##### Server status: #####
   - **Connected** under the Azure connection status for every Server.
       

        ![Azure Arc WAC](./media/Arc-2.png "Azure Arc WAC")
    
4. Now click **Arc-enabled servers** on the current **Azure Arc | Azure Stack HCI registration** page
  
    ![Azure Arc WAC](./media/Arc-3.png "Azure Arc WAC")
  
5. On the **Azure Arc | Arc-enabled servers** page, click on **AzurestackHCI-ArcServers**. 
    
    ![Azure Arc WAC](./media/Arc-4a.png "Azure Arc WAC")

6. The Azure Portal will open in an extra browser Tab, showing you the **AzurestackHCI** resource group content. On the **Resources** page in the Azure Portal, you see the two Azure Arc-enabled Server representations of the Azure Stack HCI cluster nodes.
    
    ![Azure Arc WAC](../media/hyd34.png "Azure Arc WAC")

7. Move back to the Windows Admin Center browser Tab and click on **Azure Stack HCI registration**
    
    ![Azure Arc WAC](./media/Arc-4c.png "Azure Arc WAC") 

8. On the **Azure Arc | Azure Stack HCI registration** page, click on **AzurestackHCI**.

    ![Azure Arc WAC](./media/Arc-4d.png "Azure Arc WAC") 

9. The Azure Portal will open in an extra browser Tab, showing you the **AzurestackHCI** resource group content. On the **Resources** page in the Azure Portal, click on the **HCIBox-Cluster**.

    > **NOTE**: You potentially will be asked to provide the Azure credentials. You can find them in the Environment Details of this Lab. If you get an "Action Required" screen, click "Ask later".

    ![Azure Arc WAC](../media/hyd35.png "Azure Arc WAC")

10.  The Azure Portal will open the HCIBox-Cluster - Azure Stack HCI blade. Click **Capabilities**.

        ![Azure Arc WAC](../media/hyd36.png "Azure Arc WAC")

15. On the **Capabilities** tab, click on **Windows Admin Center**.

    ![Azure Arc WAC](../media/hyd37.png "Azure Arc WAC")    

16. On the **Windows Admin Center (preview)** page, click on **Set up**.
  
    ![Azure Arc WAC](../media/hyd38.png "Azure Arc WAC")

17. On the **Windows Admin Center** page, click on **Install**.
  
    ![Azure Arc WAC](./media/Arc-13.png "Azure Arc WAC")

18. On the **Capabilities** tab, the Windows Admin Center box should indicate **Configured**.

    > **NOTE**: This can take a couple of minutes, please be patient.
  
      ![Azure Arc WAC](./media/Arc-14.png "Azure Arc WAC")    

    You just finalized the Activation of a couple of Hybrid features of Azure Stack HCI.

    > **NOTE**: We skipped configuring Insights as the Cluster nodes need to be updated to the May 2023 updates.

    Once the Windows Admin Center box shows **Configured** proceed to the next Task.

Task 2: Manage Azure Stack HCI clusters using Windows Admin Center in Azure
-----------
In this step, you will prepare your Azure Stack HCI Cluster resource in Azure to be connected to it using Windows Admin Center from the Azure Portal.

### Enable all requirements so you can use Windows Admin Center in the Azure portal to manage a hybrid machine ###

1.  On the **HCIBox-cluster** page, under Settings, click **Windows Admin Center**.
   
    On the **Windows Admin Center** page, you will see a message, that you must be part of the Windows Admin Center Administrator Login group to be able to connect.

    ![Azure Arc WAC](./media/Arc-17.png "Azure Arc WAC")

2. In the **"Search resources, services, and docs"** search box at the top of the Azure Portal page, type **subscription** and under **Services**, click **Subscriptions**.

    ![Azure Arc WAC](./media/Arc-18.png "Azure Arc WAC")
 
3. On the **Subscriptions** page, click on the Subscription name.

    > **NOTE**: It could be that your subscription name is different than the one in the screenshot!

    ![Azure Arc WAC](./media/Arc-19.png "Azure Arc WAC")

4. On the selected **Subscription** page, click **Resource providers**

    ![Azure Arc WAC](./media/Arc-20.png "Azure Arc WAC")    

5. On the **Resource providers** page, type **hybrid** in the filter by name box. Make sure the status of the Provider **Microsoft.HybridConnectivity** is **Registered**. If not Register now.

    ![Azure Arc WAC](./media/Arc-21.png "Azure Arc WAC")

6. On the current page, Click **Access Control (IAM)**. 

    ![Azure Arc WAC](./media/Arc-22.png "Azure Arc WAC")

7. On the **Access control (IAM)** page, Click **+ Add** and **Add role assignment**.

    ![Azure Arc WAC](./media/Arc-23.png "Azure Arc WAC")

8. On the **Add role assignment** page, under the **Role** tab, search for **Windows Admin Center Administrator Login**. Click on the role name **Windows Admin Center Administrator Login**. Click **Members**.

    ![Azure Arc WAC](./media/Arc-24.png "Azure Arc WAC")

9.  On the **Add role assignment** page, under the **Members** tab, Click **"+Select members**. Click on your Azure User. Click **Select** and then Click **Next**.

    ![Azure Arc WAC](./media/Arc-25.png "Azure Arc WAC")    

10. On the **Add role assignment** page, under the **Review + assign** tab, Click **Review + assign** at the bottom of the page.

    > **NOTE**: We have just the **Windows Admin Center Administrator Login** Role to an AAD User on the Subscription scope.

    >Learn more: https://learn.microsoft.com/en-us/windows-server/manage/windows-admin-center/azure/manage-hci-clusters

    ![Azure Arc WAC](./media/Arc-26.png "Azure Arc WAC")

11. In the **"Search resources, services, and docs"** search box at the top of the Azure Portal page, type **HCIBox-Cluster** and under **Resources**, click **HCIBox-Cluster**.

    ![Azure Arc WAC](../media/hyd39.png "Azure Arc WAC")

12. On the **HCIBox-Cluster** page, under Settings, click **Windows Admin Center** and then Click on **Connect**.

    ![Azure Arc WAC](./media/Arc-28.png "Azure Arc WAC")

13. On the **Windows Admin Center** page, complete the Username and Password field and Click Sign In.
    > **NOTE**: In case you need to provide login credentials, make sure the use the fully-qualified-DNS-domain\username format, and not the user principal name (UPN) format, like (user@fully_qualified_DNS_domain_name).

    ![Azure Arc WAC](./media/Arc-29.png "Azure Arc WAC")

If all how well you should now have a Windows Admin Center view on your Azure Stack HCI cluster, without needing a VPN or other direct connections. Feel free to look around.

   ![Azure Arc WAC](./media/Arc-30.png "Azure Arc WAC")

Task 3: Explore Azure Stack HCI Hybrid features in the Azure Portal
-----------
In this step, you will further explore extra Azure Stack HCI Hybrid features and capabilities.

At this time you should still be having the following page active in the Azure Portal. If so Click **Extensions**.

   ![Azure Arc WAC](../media/hyd40.png "Azure Arc WAC")  

### Explore Extensions ###

1. On the **Extension** page, you see that both Azure Stack HCI Cluster nodes have the **(Windows) Admin Center agent** installed. This was enabled by the steps we took in Task 1.

    ![Azure Arc WAC](./media/Arc-16.png "Azure Arc WAC")

### Configuration of The Azure Stack HCI 22H2 cluster in the Azure Portal ###

1. In the **"Search resources, services, and docs"** search box at the top of the Azure Portal page, type **HCIBox-Cluster** and under **Resources**, click **HCIBox-Cluster**.

   ![Azure Arc WAC](../media/hyd39.png "Azure Arc WAC")
      
2. On the **HCIBox-Cluster** page, under Settings, click **Configuration**.

   ![HCI Configuration](./media/Configuration-1.png "HCI Configuration")

3. On the **Configuration** page, click **Configuration**. Here you find 5 different Configuration topics. The first part you find is the Summary of your **Billing** for your Azure Stack HCI System.
  
    Here you also find the number of Physical Cores. Remember that you will only see the in the HW BIOS enabled Physical cores here. So you can optimize your cost by disabling unused physical cores in your hardware BIOS.
  
     **Learn more on:** https://learn.microsoft.com/en-us/azure-stack/hci/concepts/billing

    ![HCI Configuration](./media/Configuration-2.png "HCI Configuration")

1. The 2nd part on the same **configuration** page is where you can activate your **Azure Hybrid Benefits**.
   
   To be eligible for the **Azure Hybrid Benefits** you need to have enough Windows Server Data Center licenses with Active Software Assurance. Those licenses can be exchanged to get Azure Stack HCI and Windows Server subscriptions at no additional cost.
 
     **Learn more on:** https://learn.microsoft.com/en-us/windows-server/get-started/azure-hybrid-benefit#getting-azure-hybrid-benefit-for-azure-stack-hci

     ![HCI Configuration](./media/Configuration-3.png "HCI Configuration")        

2. The 3rd part on the **configuration** page is where you are able to purchase a **Windows Server subscription add-on**.
   
   Here you can buy subscription-based Windows Server licenses to cover your guest Virtual machines running Windows Server. You will be charged for the total number of physical cores in your cluster
 
     **Learn more on:** https://learn.microsoft.com/en-us/azure-stack/hci/manage/vm-activate#windows-server-subscription

     ![HCI Configuration](./media/Configuration-4.png "HCI Configuration")

3. The 4th part on the  **configuration** page is where you can change the **Service Health Data** level which is sent to, and collected by Microsoft. 
 
    Microsoft by default collects a basic set of system metadata necessary to keep the Azure Stack HCI service current, secure, and operating properly.
   
    **Learn more on:** https://learn.microsoft.com/en-us/azure-stack/hci/concepts/data-collection

    ![HCI Configuration](./media/Configuration-5.png "HCI Configuration")

4. The final part on the **configuration** page is where you can see if you have enabled the **Azure benefits** on your Azure Stack HCI 22H2 Cluster. 

    ![HCI Configuration](./media/Configuration-6.png "HCI Configuration") 

    Turning on Azure Benefits enables you to use these Azure-exclusive workloads on Azure Stack HCI:

    - **Windows Server Datacenter: Azure edition**
      - Version supported? 2022 edition or later
      - What it is? An Azure-only guest operating system that includes all the latest Windows Server innovations and other exclusive features.
    - **Extended Security Updates (ESUs)**
      - Version supported? October 12th, 2021 security updates or later
      - What it is? A program that allows customers to continue to get security updates for End-of-Support SQL Server and Windows Server VMs, now free when running on Azure Stack HCI.
    - **Azure Policy guest Configuration**
      - Version supported? Arc agent version 1.13 or later
      - What it is? A feature that can audit or configure OS settings as code, for both host and guest machines.
    - **Azure Virtual Desktop**
      - Version supported? For multi-session editions only. Windows 10 Enterprise multi-session or later.
      - What it is? A service that enables you to deploy Azure Virtual Desktop session hosts on your Azure Stack HCI infrastructure.

    > **Learn More on** https://learn.microsoft.com/en-us/azure-stack/hci/manage/azure-benefits

<!--
### Monitor Insights on your Azure Stack HCI clusters using Azure  ### 

In Task 1 of Exercise 2 you enabled the Monitoring Insights capabilities on the Azure Stack HCI cluster resource via the Azure Portal. Normally it takes around 15 minutes to see the first data showing up i

1. In the "Search resources, services, and docs" search box at the top of the Azure Portal page, type **hciboxcluster** and under Resources, click **hciboxcluster**.

   ![Insights Monitoring](./media/Arc-27.png "Insights Monitoring")

2. On the **hciboxcluster** page, under Monitoring, click **Insights**.

   ![Insights Monitoring](./media/Insights-1.png "Insights Monitoring")

3. On the **Insights** page, Click **Auto refresh**, which is currently **Off**. Click **5 minutes**, and Click **Apply**

   ![Insights Monitoring](./media/Insights-2.png "Insights Monitoring")

4. On the **Insights** page, Click **Health**. Notice that you see the same info you see on the Windows Admin Center Azure Stack HCI Cluster Dashboard.

    ![Insights Monitoring](./media/Insights-3.png "Insights Monitoring")
    ![Insights Monitoring](./media/Insights-4.png "Insights Monitoring")

5. Click on **PoolCapacityThresholdExceeded** to see the details about the Fault.

    ![Insights Monitoring](./media/Insights-5.png "Insights Monitoring")

6. On the **Insights** page, Click **Server**. Here you will view health and usage info for the servers in the cluster.

    ![Insights Monitoring](./media/Insights-6.png "Insights Monitoring")

7. On the **Insights** page, Click **Virtual machines**. Here you will view the state of virtual machines on each server in the cluster.
   
    ![Insights Monitoring](./media/Insights-7.png "Insights Monitoring")

8. On the **Insights** page, Click **Storage**. Here you will view the health of volumes and drives in the cluster. Drive health is at the bottom of the page
   
    ![Insights Monitoring](./media/Insights-8.png "Insights Monitoring")   
    ![Insights Monitoring](./media/Insights-9.png "Insights Monitoring") 
-->
Summary
-----------
In this exercise, you have enabled the Hybrid Azure Stack HCI Cluster features in the Azure Portal, reviewed the status of the Azure Arc services in the Windows Admin Center web portal, completed the pre-requirements to be able to connect and use the Windows Admin Center from the Azure Portal on the Azure Stack HCI Cluster, looked at the Azure Extensions on the Azure Stack HCI cluster in the Azure Portal, looked at all configuration capabilities on an Azure Stack HCI Cluster resource in the Azure Portal.
<!--
 and finally looked at the data captured by the Monitoring Insights service on the Azure Stack HCI cluster in the Azure Portal.
-->

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
