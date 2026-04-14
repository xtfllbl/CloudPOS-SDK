# Deploy AID/CAPK via TMS

### Overview

This guide provides a detailed process for adding, updating, and deploying AID and CAPK as part of the payment parameters in TMS. Specifically tailored for payment parameter configurations, the following steps are primarily focused on AID. It's important to note that the procedure for CAPK follows a similar pattern, ensuring a cohesive and efficient management experience within TMS environment.

### Steps

#### Accessing AlD Profile & Data

1. Navigate to Parameters > AlD Profile & AlD Data. This will lead you to the AlD Profle & AlD Data page.

&#x20;![](<../../.gitbook/assets/image (47).png>)

**Adding AlD Data**

1. Select the AlD Data tab and click the Add icon. This opens the AlD Data page.![](<../../.gitbook/assets/image (48).png>)
2. After entering necessary information, click the Commit button to create the AlD Data.

**Creating AlD Profile**

1. Switch to the AlD Profile tab and click the Add icon, leading to the AlD Profile page. ![](<../../.gitbook/assets/image (49).png>)
2. Fill in the required details and click the Commit button to create the AlD Profile.

#### Setting Up Prototype

1. Go to Parameters > ProtoType. This takes you to the ProtoType page.![](<../../.gitbook/assets/image (50).png>)
2.  Click the Add icon, fill in details on the Add ProtoType page, and commit the changes. The sample file , please download [here](https://ftp.wizarpos.com/advanceSDK/basicpaymentpramtemplate.xml).

    <figure><img src="../../.gitbook/assets/image (51).png" alt=""><figcaption></figcaption></figure>

#### Template & Profile Configuration

1. Select Parameters > Template & Profile to access the Template List page.![](<../../.gitbook/assets/image (52).png>)
2. To add a template, click the Add icon and enter details on the Add Template page. Commit to create the template![](<../../.gitbook/assets/image (53).png>)
3. Configure the template by selecting it and clicking the Configure icon. Commit the changes after configuration![](<../../.gitbook/assets/image (54).png>)

#### Managing Terminal Payment Parameters

1. Navigate to Parameters > Terminal Payment Parameter for the parameter list.
2. To add a payment parameter, click the Add icon and enter details on the respective page. Commit to create the parameter![](<../../.gitbook/assets/image (55).png>)
3. To modify a payment parameter, select it, make changes (including selecting the correct AlD orCAPK), and commit the modifications![](<../../.gitbook/assets/image (56).png>)
4. Deploy the parameter by clicking the Deploy Parameter button.![](<../../.gitbook/assets/image (57).png>)

#### Reviewing Deployed Payment Parameters

1. To view deployed parameters, select Parameters > Deployed Payment Parameter![](<../../.gitbook/assets/image (58).png>)
