# Working with Archive project

The Archive project of the vStorage storage service is a project that uses the Archive class to store data. Archive class is the third storage class of vStorage besides Gold class and Silver class. The Archive class is designed by us to be used as a safe, durable storage facility at an extremely low cost, suitable for your long-term data storage and backup needs.

With Archive class, the SLA rate is always guaranteed to reach 99.99% along with data security features according to enterprise data safety standards. Besides, the storage cost of the Archive class is the lowest among the three classes, which can help you save a lot of costs compared to other backup storage solutions. Not only that, the Archive class also aims to optimize your convenience by making data available for immediate download without any waiting time. Additionally, data management is easy on the vStorage Portal interface along with convenient search features. Similar to other vStorage classes, the Archive class is also compatible with 3rd party software so you can integrate and use it on your familiar software.

#### Some common use cases of Archive project <a href="#workingwitharchiveproject-somecommonusecasesofarchiveproject" id="workingwitharchiveproject-somecommonusecasesofarchiveproject"></a>

* Data is stored for backup purposes.
* Data that does not need to be accessed or manipulated frequently (cold data).
* Data does not require high read/write speed.
* Data can be compressed before saving to vStorage archive and when needed, users will download the compressed data and extract it for work.
* Data must be stored for at least N months, with no frequent deletion required.

#### General rules of Archive class <a href="#workingwitharchiveproject-generalrulesofarchiveclass" id="workingwitharchiveproject-generalrulesofarchiveclass"></a>

To meet the criteria of extremely low costs and service quality reflected in the 99.99% commitment SLA, Archive class has the following storage regulations:

* You can only purchase **Archive class** storage packages through **vStorage Portal**.
* You can only create containers with the **Archive class** through **vStorage Portal**. You should not use 3rd party software to create new containers because then containers will be created with the default **Gold class**.
* During the first **24 hours** from the time you upload a file to the Archive class, if your uploaded files are not correct, you can delete them. After these 24 hours, the data will not be deleted until the specified period of at least 6 months has passed as specified below.
* Data uploaded to this archive class will not be deleted until it has reached a lifespan of at least **6 months**. We will still allow you to perform other actions on this data including: copy, move, rename, share, set tags, set metadata, upload alternative files).
* Archive class provides and fully supports tools for use including: **vStorage Portal, vStorage API, 3rd party software**. However, deleting data can only be done through **vStorage Portal**.
* For data recovery needs: the file will be ready for download within **1-12 hours**. Costs for operations are clearly specified when you purchase resources, for details see How to calculate fees.

#### Tips when using <a href="#workingwitharchiveproject-tipswhenusing" id="workingwitharchiveproject-tipswhenusing"></a>

* Make sure the data you put into the Archive class is data that needs to be stored but is rarely used. Because although the storage cost of the Archive class is the lowest, the costs arise from manipulating data such as deleting, restoring, etc. will be 1-2 times higher than Gold class and Silver class storage classes.
* The Archive class is also not suitable for storing constantly changing data because of our 6-month data deletion restriction. If you need to store backup data but have time to change data every week or month, Silver class will be the right choice.

\
