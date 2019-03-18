General Steps Deploy on Azure Portal
---------------------------
This guide describes how to install and set up Ant Media Server on a Microsoft Azure Marketplace  Ubuntu 16.04 virtual machine instance. This tutorial assumes that you have an Azure account, or a trial account.

Step 1: Create a Virtual Machine
--------------------------------
Firstly, click Create a resource in `Azure Dashboard <https://portal.azure.com>`_.

.. figure:: https://antmedia.io/wp-content/uploads/2019/03/create-resource-azure-marketplace.jpg
   :alt: Create a resource in Azure Dashboard
 
After clicking on Create a resouce, you will see the new Marketplace page. Please write “Ant Media Server” to the search side. 

.. figure:: https://antmedia.io/wp-content/uploads/2019/03/ant-media-server-azure-marketplace-listing.jpg
   :alt: Azure Marketplace listing Ant Media Server

Choose one of Ant Media Server Community Edition or Enterprise Edition.

.. figure:: https://antmedia.io/wp-content/uploads/2019/03/azure-marketplace-ant-media-server.jpg
   :alt: Azure Marketplace listing Ant Media Server

.. tip::
	Community Edition and Enterprise Edition comparison chart is `here <https://antmedia.io/#comparison_table>`_.

Step 2: Customize Virtual Machine
--------------------------------
Part 1 – “Basics” in Create a Virtual Machine
^^^^^^^^^^^^^^^^^^^^^
.. figure:: https://antmedia.io/wp-content/uploads/2019/03/basics-in-azure-marketplace.jpg
   :alt: Basics section in Azure Marketplace Virtual Machine

**In Subscription**, Azure default payment method is Pay-As-You-Go. More details for see this `link <https://azure.microsoft.com/en-us/offers/ms-azr-0003p>`_.

**In Resource group**, specify the resource group. To select an existing resource group, click Use existing, and then click the arrow in the list box to reveal existing resource groups. To create a new resource group, click Create new, and then type a name for it in the list box. For details, see `Manage resource groups <https://docs.microsoft.com/tr-tr/azure/azure-resource-manager/manage-resources-portal#manage-resource-groups>`_.

**In Virtual machine name**, enter a name for your virtual machine. ("name must be 1-64 characters long and it cannot contain non-ASCII and special characters.") 

**In Region**, select the region where the virtual machine instance will be located. It's best to select a location that has the lowest latency to a camera or encoder that's delivering a live stream to Ant Medai Server.

**In Image**, will see your selected image.

**In VM disk type**, choose a disk type. Azure solid state disks (SSD) are backed by solid state drives and offer consistent, low latency performance. They provide the best balance between price and performance and are ideal for I/O-intensive applications and production workloads. 

**In User name**, type the name of the account that you'll use to administer the virtual machine (you can't use root for the user name). Then under Authentication type, click SSH public key and copy and paste an OpenSSH public key that will be used to authenticate the account user name.

.. tip::
	Note: You can generate an OpenSSH public key with tools like ssh-keygen on Linux and OS X or PuTTYgen on Windows. For details, see `Create and use an SSH public-private key pair for Linux VMs in Azure <https://azure.microsoft.com/documentation/articles/virtual-machines-linux-use-ssh-key/>`_.


Part 2 – “Disks” in Create a Virtual Machine
^^^^^^^^^^^^^^^^^^^^^
.. figure:: https://antmedia.io/wp-content/uploads/2019/03/disks-in-azure-marketplace.jpg
   :alt: Disks section in Azure Marketplace Virtual Machine

**In OS disk type**, Effective at input speeds I/O. 
Premium SSD disks offer high-performance, low-latency disk support for I/O-intensive applications and production workloads. 

Standard SSD Disks are a cost effective storage option optimized for workloads that need consistent performance at lower IOPS levels. 

Use Standard HDD disks for Dev/Test scenarios and less critical workloads at lowest cost.

.. tip::
	We recommend Premium SSD for high I/O.

Part 3 – “Networking”  in Create a Vitual Machine
^^^^^^^^^^^^^^^^^^^^^ 

.. figure:: https://antmedia.io/wp-content/uploads/2019/03/networking-in-azure-marketplace.jpg
   :alt: Networking section in Azure Marketplace Virtual Machine

**In Virtual Network**, currently selected subscription and location are listed.  If you choose to create a new virtual network, it will be created in the same subscription, location, and resource group as the storage account. Virtual networks in a different subscription, and/or paired failover location, may be specified after storage account creation.

**In Subnet**, listed in default value of your  Virtual Network.

**In Public IP**, communicate with Virtual Machine from outside the Virtual Network.

**In Configure network security group**, the most important configuration is here. Here is the TCP and UDP port, inbound and outbound permissions are configured. If you change port setting in Ant Media Server, you need to change “Configure network security group”. Ant Media Server default port values listed in below.

.. warning::
	**The following ports to the Inbound list in Ant Media Server:**

	* TCP:1935 (RTMP)
	* TCP:5080 (HTTP)
	* TCP:5443 (HTTPS)
	* TCP:5554 (RTSP)
	* UDP:5000-65000 (WebRTC and RTSP)

Part 4 – “Management” in Create Virtual Machine
^^^^^^^^^^^^^^^^^^^^^
.. figure:: https://antmedia.io/wp-content/uploads/2019/03/management-in-azure-marketplace.jpg
   :alt: Management section in Azure Marketplace Virtual Machine

Configure monitoring and management options for your Virtual Machine

Part 5 – “Guest Config” in Create Virtual Machine
^^^^^^^^^^^^^^^^^^^^^
.. figure:: https://antmedia.io/wp-content/uploads/2019/03/guest-config-in-azure-marketplace.jpg
   :alt: Guest Config section in Azure Marketplace Virtual Machine

Here is Extensions and Cloud Init options. 

Extension means using in server applications like Acronis Backup. 

Ant Media Server image doesn’t support cloud init.

Part 6 – “Tags” in Create Virtual Machine
^^^^^^^^^^^^^^^^^^^^^
.. figure:: https://antmedia.io/wp-content/uploads/2019/03/tags-in-azure-marketplace.jpg
   :alt: Tags Config section in Azure Marketplace Virtual Machine

Tags are name/value pairs that enable you to categorize resources and view consolidated billing by applying the same tag to multiple resources and resource groups.

Part 7 – “Review + Create” in Create Virtual Machine
^^^^^^^^^^^^^^^^^^^^^
.. figure:: https://antmedia.io/wp-content/uploads/2019/03/review-create-in-azure-marketplace.jpg
   :alt: Review + Create section in Azure Marketplace Virtual Machine

Here you will see the settings you have made in other sections.
After checking all the settings you can create the virtual machine.
