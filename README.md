# IBM Cloud Helper API
IBM Cloud Helper is a collection of APIs that make it easy to perform common tasks for managing and configuring IBM Cloud Services.  This will be a living list of APIs that will grow over time.  If you would like to contribute and add an API that you find useful or have an idea of a nice to have api please let @kevincollins know.

<h3>Current list of APIs</h3>

**1. IBM Cloud Satellite**   
  * Create a demo environment for IBM Cloud Satellite  
  * Retrieve the private SSH Key for the demo environment   
  * Delete all resources created in the demo environment  

**2. Cloud Object Storage**  
  * Copy the contents of a COS Bucket to another bucket  
  * Retrieve a list of buckets and metadata  
  * Retrieve Metadata for a bucket  
  * Add Metadata to a bucket  
  * Create a PVC on a Kubernetes cluster that is attached to COS Bucket  
  * Delete a COS bucket and all objects in it  
  * Load buckets from a COS instance into redis - for fast retrieval  

**3. CloudPak for Data**  
   * CloudPak for Data Pre-Installation Script  

**4. VPC Infrastructure**  
    * Create and attach block devices to VPC Cluster  
    * Delete block devices attached to a VPC Cluster  
    * Retrieve a list of block devices attaced to a VPC Cluster  
    
**5. General Utility**  
    * Remove inactive users from an account  
    * Delete a resource group and ALL resources in the resource group  

**6. Classic Infrastructure**  
    * Create and attach block storage devices to an OpenShift cluster  

**7. OpenShift**  
    * Get a login token for OpenShift  
    * Get a list of OpenShift versions supported by IBM Cloud  

--

For detailed documentation on the APIs and to try out the APIs, please visit the swagger page.
[https://api.ibmcloudhelper.com:8000/swagger]()


[PostMan Collection](https://www.ibmcloudhelper.com/IBM-Cloud-Helper.postman_collection.json)