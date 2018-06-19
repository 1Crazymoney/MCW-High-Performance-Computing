![](https://github.com/Microsoft/MCW-Template-Cloud-Workshop/raw/master/Media/ms-cloud-workshop.png "Microsoft Cloud Workshops")

<div class="MCWHeader1">
Big Compute
</div>

<div class="MCWHeader2">
Whiteboard design session trainer guide
</div>

<div class="MCWHeader3">
March 2018
</div>

Information in this document, including URL and other Internet Web site references, is subject to change without notice. Unless otherwise noted, the example companies, organizations, products, domain names, e-mail addresses, logos, people, places, and events depicted herein are fictitious, and no association with any real company, organization, product, domain name, e-mail address, logo, person, place or event is intended or should be inferred. Complying with all applicable copyright laws is the responsibility of the user. Without limiting the rights under copyright, no part of this document may be reproduced, stored in or introduced into a retrieval system, or transmitted in any form or by any means (electronic, mechanical, photocopying, recording, or otherwise), or for any purpose, without the express written permission of Microsoft Corporation.

Microsoft may have patents, patent applications, trademarks, copyrights, or other intellectual property rights covering subject matter in this document. Except as expressly provided in any written license agreement from Microsoft, the furnishing of this document does not give you any license to these patents, trademarks, copyrights, or other intellectual property.

The names of manufacturers, products, or URLs are provided for informational purposes only and Microsoft makes no representations and warranties, either expressed, implied, or statutory, regarding these manufacturers or the use of the products with any Microsoft technologies. The inclusion of a manufacturer or product does not imply endorsement of Microsoft of the manufacturer or product. Links may be provided to third party sites. Such sites are not under the control of Microsoft and Microsoft is not responsible for the contents of any linked site or any link contained in a linked site, or any changes or updates to such sites. Microsoft is not responsible for webcasting or any other form of transmission received from any linked site. Microsoft is providing these links to you only as a convenience, and the inclusion of any link does not imply endorsement of Microsoft of the site or the products contained therein.
© 2018 Microsoft Corporation. All rights reserved.

Microsoft and the trademarks listed at https://www.microsoft.com/en-us/legal/intellectualproperty/Trademarks/Usage/General.aspx are trademarks of the Microsoft group of companies. All other trademarks are property of their respective owners.

**Contents**

<!-- TOC -->

- [Big Compute whiteboard design session student guide](#big-compute-whiteboard-design-session-student-guide)
    - [Abstract and learning objectives](#abstract-and-learning-objectives)
    - [Step 1: Review the customer case study](#step-1-review-the-customer-case-study)
        - [Customer situation](#customer-situation)
        - [Customer needs](#customer-needs)
        - [Customer objections](#customer-objections)
        - [Infographic for common scenarios](#infographic-for-common-scenarios)
    - [Step 2: Design a proof of concept solution](#step-2-design-a-proof-of-concept-solution)
    - [Step 3: Present the solution](#step-3-present-the-solution)
    - [Wrap-up](#wrap-up)
    - [Additional references](#additional-references)

<!-- /TOC -->

#  Big Compute whiteboard design session student guide

## Abstract and learning objectives 

Setup and configure a scale-out media processing architecture using Azure Batch. You will use big compute (scale-out compute, embarrassingly parallel processing) techniques without having to write a lot of code, learning how these tasks can be accomplished declaratively.

Learning Objectives:

-   Learn the core capabilities of Azure Batch

-   Understand how to author custom Pool and Job templates

-   Work with Job input and output files

-   Learn to author Batch auto-scale formulas

-   Leverage Batch Labs and the Azure Portal for management and monitoring

-   Use Marketplace applications to simplify common big compute tasks, such as 3D rendering

## Step 1: Review the customer case study 

**Outcome** 

Analyze your customer’s needs.
Time frame: 15 minutes 
Directions: With all participants in the session, the facilitator/SME presents an overview of the customer case study along with technical tips. 
1.  Meet your table participants and trainer 
2.  Read all of the directions for steps 1–3 in the student guide 
3.  As a table team, review the following customer case study

### Customer situation

ThoughtRender provides image and video processing services to many industries -- marketing and advertising, retail, medical, and media and entertainment. You know those furniture magazines you love to look at? Most of the pictures in these magazines are generated by the HPC compute clusters at ThoughtRender. Their unique ability to tie together industry solutions into a reliable service for their customers (e.g., furniture magazine designers! 3D animated movie makers!), together with their in-house knowledge on image and video, is a quality service that sets them apart from competitors.

ThoughtRender currently operates their own, on-premises services (with their own on-premises HPC clusters, and other IT infrastructure), but their success has led to challenges in terms of their growth, and ability to scale to new jobs, and new industries. They are curious about cloud and think that not only could it help them scale, but help them improve costs and pass savings to customers, address the seasonality of rendering demand (by only paying for resources when actually used) and to take advantage of new technologies, such as the latest GPUs.

Customers often ask questions like, "Could you get that job processed this week, instead of in 3 weeks' time?" ThoughtRender thinks that perhaps bursting jobs to the cloud could help them deliver bigger jobs, or regular jobs quicker for their customers (e.g., in 1 day, instead of 5 days). They intend to pilot a solution to address this.

They also want to consider how to integrate with their on-premises infrastructure and operating model. They have three large on-premises HPC clusters -- one in each site -- London, New York, and Singapore. They also have labs in each site that provide high-end visualization workstations for quality control, mostly operated by internal staff, but sometimes together with customers. ThoughtRender have 3 Petabytes (PB) of data (customer assets, and working "scratch" data shares) -- 1 PB typically stored per site.

Thomas Pix, CIO of ThoughtRender is looking to modernize their story. He would love to understand how to tap into the \"power of the cloud\" to be more flexible to customer demands, but also to consider new ways of working. Lots of data is generated via their on-premises HPC clusters, which also spends a lot of time moving between sites. He would love to see if they can move this data away from their on-premises datacenter into the cloud, and enhance their ability to load, process, and analyze it going forward. Given his long-standing relationship with Microsoft, he would like to see if Azure can meet his needs.

### Customer needs 

1.  Want to be able to provide better flexibility to their customer demands (i.e., to have more work processed, or to complete work in a faster time)

2.  Want to investigate potential advantages to using cloud (e.g., latest technologies, bursting capability, cost savings)

3.  Want to integrate with their on-premises systems where possible (e.g., to burst to cloud for additional capacity)

4.  Want to collaborate and visualize the results of their work, on their own, or together with customers

### Customer objections 

1.  Will Azure give us control to schedule jobs when we want?

2.  Will the capacity be available on Azure when we want it?

3.  We heard Microsoft does Linux now. But how true is this? Will it work with our chosen Linux version?

4.  We have Petabytes of data on-premises. It would cost us a fortune and take ages to move this to the cloud!

5.  We heard collaboration is possible for 3D imaging workstations, but we have very specific color requirements and buy top-end workstation equipment for our users. Our users just wouldn\'t get the interaction performance they require with something \"remote\" in the cloud.

6.  Will this take jobs away from our IT system administrators and HPC engineers?

### Infographic for common scenarios

High-performance computing (HPC) applications can scale to thousands of compute cores, extend on-premises big compute, or run as a 100% cloud-native solution. This HPC solution is implemented with Azure Batch, which provides job scheduling, auto-scaling of compute resources, and execution management as a platform service (PaaS) that reduces HPC infrastructure code and maintenance.

![In this Common HPC scenario diagram, A Web App and Client app have bi-directional arrows pointing to Batch, which has a bi-directional arrow pointing to Virtual Machines, which has bi-directional arrows pointing to Storage. Microsoft and Linux icons also display.](images/Whiteboarddesignsessiontrainerguide-BigComputeimages/media/image2.png "Common HPC scenario diagram")

https://azure.microsoft.com/en-us/solutions/architecture/hpc-big-compute-saas/

## Step 2: Design a proof of concept solution

**Outcome** 
Design a solution and prepare to present the solution to the target customer audience in a 15-minute chalk-talk format. 

Time frame: 60 minutes

**Business needs**

Directions: With all participants at your table, answer the following questions and list the answers on a flip chart. 
1.  Who should you present this solution to? Who is your target customer audience? Who are the decision makers? 
2.  What customer business needs do you need to address with your solution?

**Design** 
Directions: With all participants at your table, respond to the following questions on a flip chart.

*High-level architecture*

1.  Without getting into the details (the following sections will address the particular details), diagram your initial vision for handling the top-level requirements for data loading, data preparation, storage, machine learning modeling, and reporting. You will refine this diagram as you proceed.

*Data loading*

1.  How would you recommend ThoughtRender get their data into (and out of) Azure? What services would you suggest and what are the specific steps they would need to take to prepare the data, to transfer the data, and where would the loaded data land?

2.  Update your diagram with the data loading process with the steps you identified.

*Video and Image Processing*

1.  What software tools will be used here? Are they commercial, or Open Source, or a combination of both? Will ThoughtRender need to throw away the tools they are already using, or are some integrations possible?

2.  For Linux based tools, does it matter which flavor of Linux is chosen?

3.  When are these tools used at ThoughtRender? Are they part of a workflow?

*Batch Computing*

1.  What technology would you recommend ThoughtRender use for implementing their rendering compute workloads in Azure?

2.  Are there particular types of compute instances you would guide ThoughtRender to use?
    
    -   Are compute-intensive, memory-intensive, disk-intensive, or network-optimized instances needed?

    -   Are GPU based instances needed?

3.  How would you guide ThoughtRender to load data so it can be processed by the rendering compute workload?

4.  How will this data be used at the beginning, middle, and end of a compute workload?

    -   Where will this data be stored?

    -   Will this data be stored on compute instances during a batch run? Would you store data on each compute node working in a batch, or would you store data in a shared area?

    -   What sort of performance will be required from this storage?

    -   Will this data need to be backed up or archived?

5.  How can ThoughtRender measure and analyze the performance of the compute workload? During and afterward?

6.  How can ThoughtRender scale and resize to be flexible to customer needs?

*Operationalizing and Integrating*

1.  Is it possible for ThoughtRender to connect their Batch Rendering workloads in Azure, to their Rendering workloads on-premises, in their various sites? If so, will the connection be made at a networking level, an operating system level, or an application level?

2.  Is it possible for ThoughtRender to keep their Azure infrastructure separate (i.e., completely unconnected) to their on-premises HPC clusters?

*Visualization and Remote Workstations*

1.  Are special types of compute instances needed for remote workstations in Azure?

2.  Is a special type of software required for client access? Could users simply use remote desktop? Would this perform the way ThoughtRender (or their customers) would like it to?

    -   Would it be secure?

    -   Would it be color correct?

    -   Would it perform?

    -   Would it allow collaboration or interactivity?

**Prepare**

Directions: With all participants at your table: 

1.  Identify any customer needs that are not addressed with the proposed solution. 
2.  Identify the benefits of your solution. 
3.  Determine how you will respond to the customer’s objections. 

Prepare a 15-minute chalk-talk style presentation to the customer. 

## Step 3: Present the solution

**Outcome**
 
Present a solution to the target customer audience in a 15-minute chalk-talk format.

Time frame: 30 minutes

**Presentation** 

Directions:
1.  Pair with another table.
2.  One table is the Microsoft team and the other table is the customer.
3.  The Microsoft team presents their proposed solution to the customer.
4.  The customer makes one of the objections from the list of objections.
5.  The Microsoft team responds to the objection.
6.  The customer team gives feedback to the Microsoft team. 
7.  Tables switch roles and repeat Steps 2–6.

##  Wrap-up 

Time frame: 15 minutes

-   Tables reconvene with the larger group to hear an SME share the preferred solution for the case study.

##  Additional references
|    |            |
|----------|:-------------:|
| **Description** | **Links** |
| HPC Solution Architectures | <https://azure.microsoft.com/en-us/solutions/high-performance-computing/#references/> |
| Rendering on Azure | <https://rendering.azure.com/> |
| Azure Batch | <https://docs.microsoft.com/en-us/azure/batch/> |
| Batch Shipyard | <https://github.com/Azure/batch-shipyard/> |
| Batch CLI extensions | <https://github.com/Azure/azure-batch-cli-extensions/> |
| Batch Labs (beta) | <https://github.com/Azure/BatchLabs/releases/> |
| AzCopy (Linux) | <https://docs.microsoft.com/en-us/azure/storage/storage-use-azcopy-linux/> |
| Azure Batch Rendering Service | <https://docs.microsoft.com/en-us/azure/batch/batch-rendering-service/> |


**Supplemental Materials**

The following projects may be helpful to you after completing the workshop in understanding other ways in which Azure Batch can be applied, besides media and rendering.
|    |            |
|----------|:-------------:|
| **Description** | **Links** |
| CycleCloud Lab | <https://github.com/azurebigcompute/BigComputeLabs/tree/master/CycleCloud/> |
| Do Azure Parallel R Package | <https://github.com/Azure/doAzureParallel/> |
| Big Compute Batch VM | <https://github.com/mkiernan/bigcomputebench/> |
