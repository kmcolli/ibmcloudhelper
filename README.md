# IBM Cloud Helper API
IBM Cloud Helper is a collection of APIs that make it easy to perform common tasks for managing and configuring IBM Cloud Services.  This will be a living list of APIs that will grow over time.  If you would like to contribute and add an API that you find useful or have an idea of a nice to have api please let @kevincollins know.

There are seven categories of APIs:
* Cloud Object Storage
* CloudPak for Data
* VPC Infrastructure
* General Utility
* Classic Infrastructure
* Portworx
* OpenShift

For detailed documentation on the APIs, please visit the swagger page.
https://swagger.ibmcloudhelper.com

Postman Collection:
*coming soon*

Common API Endpoint:  
**api.ibmcloudhelper.com:8000**
## Cloud Object Storage

### Retrieve a list of COS Buckets
Retrieves a list of buckets including metadata for the bucket and the size of the bucket.  Search criteria includes searching by name and metadata.  

API Endpoint:
**POST /api/v1/getBuckets/**  

Example Payload

```
{ "search_text": "",     
  "metadata": {},  
  "cos_apikey": "",  
  "cos_instanceid": "",  
  "cos_endpoint": ""  
}
```   

**search_text:** text to search bucket names for  

**metadata**  metadata of the bucket to search for  
	example:
	
	
	metadata": { "cp": "cp4d",
				 "custom tag": "version 3.1" }
			
**cos_apikey (optional)**  apikey of your IBM Cloud Account where you COS instance is located  
If not included, the *getroks* COS instance will be used.

**cos_instanceid (optional)**  COS Instance Id 
If not included, the *getroks* COS instance will be used.
			
**cos_endpoint (optional)**  COS Endpoint where the bucket is located
	
example:
		
	"cos_endpoint": "https://s3.us-east.cloud-object-storage.appdomain.cloud"
	 
If not included, the *getroks* COS instance will be used.			
example usage:

	curl -X POST -H "Content-Type: application/json" 'api.ibmcloudhelper.com:8000/api/v1/getBuckets/' -d '{"search_text": "", "metadata": {''}}'
	
*note: bucket metadata is read by looking for a README object in the bucket where metatdata is set on this object.

### Delete COS Bucket and all Objects
Single API call that deletes all objects in a bucket and the bucket itself.

API Endpoint:
**POST /api/v1/deleteCosBucket/**  

Example Payload

```
{ "bucket_name": "",     
  "cos_apikey": "",  
  "cos_instanceid": "",  
  "cos_endpoint": "",
  "cos_access_id": "",
  "cos_access_key": "" 
}
```   

**bucket_name:** name of the bucket to delete  

**cos_apikey (optional)**  apikey of your IBM Cloud Account where you COS instance is located  
If not included, the *getroks* COS instance will be used.

**cos_instanceid (optional)**  COS Instance Id 
If not included, the *getroks* COS instance will be used.
			
**cos_endpoint (optional)**  COS Endpoint where the bucket is located
	
example:
	
	"cos_endpoint": "https://s3.us-east.cloud-object-storage.appdomain.cloud"
	 
**cos_access_id (optional)**  COS HMAC Access Id 
If not included, the *getroks* COS instance will be used.
			
**cos_access_key (optional)**  COS HMAC Access Key

If not included, the *getroks* COS instance will be used.			
example usage:

	curl -X POST -H "Content-Type: application/json" 'api.ibmcloudhelper.com:8000/api/v1/deleteCosBucket/' -d '{"bucket_name": ""}'
	
*note: all objects in the bucket will be delete along with the bucket itself
			
### Add Metadata to COS Bucket
Adds metadata to a bucket by creating a file called README file in the bucket that contains key value pairs.  Metadata given to the API call will overwrite the existing metadata.

API Endpoint:
**POST /api/v1/addCOSMetadata/**  

Example Payload

```
{ "bucket_name": "", 
  "metadata": {},    
  "cos_apikey": "",  
  "cos_instanceid": "",  
  "cos_endpoint": "",
  "cos_access_id": "",
  "cos_access_key": "" 
}
```   

**bucket_name:** name of the bucket to add metadata to

**metadata**  metadata of the bucket to search for  
	example:
	
	metadata": { "cp": "cp4d",
					 "custom tag": "version 3.1" } 

**cos_apikey (optional)**  apikey of your IBM Cloud Account where you COS instance is located  
If not included, the *getroks* COS instance will be used.

**cos_instanceid (optional)**  COS Instance Id 
If not included, the *getroks* COS instance will be used.
			
**cos_endpoint (optional)**  COS Endpoint where the bucket is located  
	example:
	
	"cos_endpont": "https://s3.us-east.cloud-object-storage.appdomain.cloud"
	 
**cos\_access_id (optional)**  COS HMAC Access Id 
If not included, the *getroks* COS instance will be used.
			
**cos\_access_key (optional)**  COS HMAC Access Key

If not included, the *getroks* COS instance will be used.			
example usage:

	curl -X POST -H "Content-Type: application/json" 'api.ibmcloudhelper.com:8000/api/v1/deleteCosBucket/' -d '{"bucket_name": "", "metadata": {"cp": "cp4d"}}'
	
*note: metadata is stored in a README object in the bucket

### Retrieve a List of COS Metadata for a Bucket
Retrieves a list of metadata for a bucket by reading a file name README containing key value pairs.

API Endpoint:
**POST /api/v1/getCOSMetadata/**  

Example Payload

```
{ "bucket_name": "", 
  "cos_apikey": "",  
  "cos_instanceid": "",  
  "cos_endpoint": ""
}
```   

**bucket_name:** name of the bucket to add metadata to


**cos_apikey (optional)**  apikey of your IBM Cloud Account where you COS instance is located  
If not included, the *getroks* COS instance will be used.

**cos_instanceid (optional)**  COS Instance Id 
If not included, the *getroks* COS instance will be used.
			
**cos_endpoint (optional)**  COS Endpoint where the bucket is located
	
example:
	
	"cos_endpoint": "https://s3.us-east.cloud-object-storage.appdomain.cloud"
	 

If not included, the *getroks* COS instance will be used.			
example usage:

	curl -X POST -H "Content-Type: application/json" 'api.ibmcloudhelper.com:8000/api/v1/getCOSMetadata/' -d '{"bucket_name": ""}'
	
*note: metadata is read from a README object in the bucket

### Copy a COS Bucket to Another Bucket
Single API that directly copies one bucket to another in the same COS instance.

API Endpoint:
**POST /api/v1/copyCosMetadata/**  

Example Payload

```
{ "source_bucket": "",
  "destination_bucket": "", 
  "cos_apikey": "",  
  "cos_instanceid": "",  
  "cos_endpoint": "",
  "cos_access_id": "",
  "cos_access_key": "" 
 }
```   

**bucket_name:** name of the bucket to add metadata to


**cos_apikey (optional)**  apikey of your IBM Cloud Account where you COS instance is located  
If not included, the *getroks* COS instance will be used.

**cos_instanceid (optional)**  COS Instance Id 
If not included, the *getroks* COS instance will be used.
			
**cos_endpoint (optional)**  COS Endpoint where the bucket is located
	
example:
	
	"cos_endpoint": "https://s3.us-east.cloud-object-storage.appdomain.cloud"
	 
**cos\_access_id (optional)**  COS HMAC Access Id 
If not included, the *getroks* COS instance will be used.
			
**cos\_access_key (optional)**  COS HMAC Access Key

If not included, the *getroks* COS instance will be used.			
example usage:

	curl -X POST -H "Content-Type: application/json" 'api.ibmcloudhelper.com:8000/api/v1/copyCosMetadata/' -d '{"source_bucket": "", "destination_bucket": "" }'
	
### Create a COS PVC on a ROKS Cluster
This api will do the following:

* Install the ibm-object-storage helm chart on a ROKS Cluster
* Create a COS bucket if not already created
* Create a secret in ROKS to acess the COS Bucket
* Create a pvc attached to the ROKS cluster
	
API Endpoint:
**POST /api/v1/Create_cosPVC/**  

Example Payload

```
{ "apikey": "",
  "cluster_name": "", 
  "project": "",
  "pvc": "",
  "bucket": "",  
  "cos_apikey": "",
  "cos_instanceid": "",  
  "cos_endpoint": ""
 }
```   

**apikey:** apikey of your IBM Cloud Account where your ROKS cluster is located

**cluster_name:** name of your ROKS cluster

**project:** name of your OpenShift Project where the PVC will be created

**pvc:** name of the pvc to be created

**bucket:** name of the COS bucket to create or use if already created

**cos_apikey (optional)**  apikey of your IBM Cloud Account where you COS instance is located  
If not included, the *getroks* COS instance will be used.

**cos_instanceid (optional)**  COS Instance Id 
If not included, the *getroks* COS instance will be used.
			
**cos_endpoint (optional)**  COS Endpoint where the bucket is located
	
example:
	
	"cos_endpoint": "https://s3.us-east.cloud-object-storage.appdomain.cloud"
	 			
example usage:

	curl -X POST -H "Content-Type: application/json" 'api.ibmcloudhelper.com:8000/api/v1/Create_cosPVC/' -d '{"apikey": "", "cluster_name": "", "project": "", "pvc": "", "bucket": "" }'

## Cloud Pak for Data

### Add Certificates to Cloud Pak for Data
* Creates a dns entry in cloud internet services mapping ```cp4d-<cluster_name>.ibmcloudroks.net ```to the cp4d console route that references the cluster ingress subdomain.
* updates CP4D nginx pods with ibmcloudroks.net certificates
* updates the cp4d route to point to the secured URL  

API Endpoint:
**POST /api/v1/cp4d_addGetRoksCerts/**  

Example Payload

```
{ "apikey": "",
  "cluster_name": "", 
  "cp4d_project": "",
} 
```
**apikey:** apikey of your IBM Cloud Account where your ROKS cluster is located

**cluster_name:** name of your ROKS cluster

**cp4d_project:** name of your OpenShift Project where the CP4D is running
			
example usage:

	curl -X POST -H "Content-Type: application/json" 'api.ibmcloudhelper.com:8000/api/v1/cp4d_addGetRoksCerts/' -d '{"apikey": "", "cluster_name": "", "cp4d_project": ""}'
	
	
### Update Certificates for Cloud Pak for Data
* updates the CP4D nginx pods with ibmcloudroks.net certificates

API Endpoint:
**POST /api/v1/cp4d_updateGetRoksCerts/**  

Example Payload

```
{ "apikey": "",
  "cluster_name": "", 
  "cp4d_project": "",
} 
```
**apikey:** apikey of your IBM Cloud Account where your ROKS cluster is located

**cluster_name:** name of your ROKS cluster

**cpd_project:** name of your OpenShift Project where the CP4D is running
			
example usage:

	curl -X POST -H "Content-Type: application/json" 'api.ibmcloudhelper.com:8000/api/v1/cp4d_updateGetRoksCerts/' -d '{"apikey": "", "cluster_name": "", "cp4d_project": ""}'
	
### Run CP4D Pre-installation Script
* runs the cp4d pre-installation script before you can install cp4d with IBM Cloud Schematics
* optimizes CP4D by setting linux worker node parameters no root squash and setting the kernel semaphore.

API Endpoint:
**POST /api/v1/cp4d_preinstallation/**  

Example Payload

```
{ "apikey": "",
  "cluster_name": ""
} 
```

**apikey:** apikey of your IBM Cloud Account where your ROKS cluster is located

**cluster_name:** name of your ROKS cluster
			
example usage:

	curl -X POST -H "Content-Type: application/json" 'api.ibmcloudhelper.com:8000/api/v1/cp4d_preinstallation/' -d '{"apikey": "", "cluster_name": ""}'
	
## VPC

### Attach raw block devices to ROKS Worker Nodes on a VPC
* creates raw block devices on VPC Gen 2 in each zone the worker nodes are in
* attaches the created block devices to ROKS worker nodes
* works in both MZR and SZR

API Endpoint:  
**POST /api/v1/attachBlockVPC/**  

Example Payload

```
{ "apikey": "",
  "cluster_name": ""
} 
```
**apikey:** apikey of your IBM Cloud Account where your ROKS cluster is located

**cluster_name:** name of your ROKS cluster
			
example usage:

	curl -X POST -H "Content-Type: application/json" 'api.ibmcloudhelper.com:8000/api/v1/attachBlockVPC/' -d '{"apikey": "", "cluster_name": "" }'

### Delete raw block devices to ROKS Worker Nodes on a VPC
* unattaches block devices created with the *attachBlockVPC* api.
* deletes block devices

API Endpoint:  
**POST /api/v1/deleteBlockVPC/**  

Example Payload

```
{ "apikey": "",
  "cluster_name": ""
} 
```
**apikey:** apikey of your IBM Cloud Account where your ROKS cluster is located

**cluster_name:** name of your ROKS cluster
			
example usage:

	curl -X POST -H "Content-Type: application/json" 'api.ibmcloudhelper.com:8000/api/v1/deleteBlockVPC/' -d '{"apikey": "", "cluster_name": "" }'	

### Get list of block devices attached to ROKS Worker Nodes on a VPC
* retrieves a list of block devices attached to worker nodes on a VPC.

API Endpoint:  
**POST /api/v1/getBlockVPC/**  

Example Payload

```
{ "apikey": "",
  "cluster_name": ""
} 
```
**apikey:** apikey of your IBM Cloud Account where your ROKS cluster is located

**cluster_name:** name of your ROKS cluster
			
example usage:

	curl -X POST -H "Content-Type: application/json" 'api.ibmcloudhelper.com:8000/api/v1/getBlockVPC/' -d '{"apikey": "", "cluster_name": "" }'
	
## Classic

### Remove unused block volumes on classic infrastructure
* removes all block volumes not attached to a kubernetes cluster
* *warning - this is destructive and will immediate delete all block volumes that are not being used by Kubernetes.  Only run this if you are sure you are not using block volumes outside of Kuberenetes

API Endpoint:  
**POST /api/v1/removeUnusedBlock/**  

Example Payload

```
{ "apikey": "",
  "cluster_name": ""
} 
```
**apikey:** apikey of your IBM Cloud Account where your ROKS cluster is located

**cluster_name:** name of your ROKS cluster
			
example usage:

	curl -X POST -H "Content-Type: application/json" 'api.ibmcloudhelper.com:8000/api/v1/removeUnusedBlock/' -d '{"apikey": "", "cluster_name": "" }'

## Portworx

### Provision portworx using the IBM Cloud Catalog
* Creates a portworx instance for a given cluster
* Portworx instance is created in the same resource group as the cluster
* Assumes raw block storage devices are already created. 

API Endpoint:  
**POST /api/v1/createPxIBMCatalog/**  

Example Payload

```
{ "apikey": "",
  "cluster_name": ""
} 
```
**apikey:** apikey of your IBM Cloud Account where your ROKS cluster is located

**cluster_name:** name of your ROKS cluster
			
example usage:

	curl -X POST -H "Content-Type: application/json" 'api.ibmcloudhelper.com:8000/api/v1/cp4d3_createPx/' -d '{"apikey": "", "cluster_name": "" }'

### Create Block Storage on Classic
* Installs the IBM Block Attacher Helm chart into the given cluster
* For each worker node in the cluster the following is performed:
    * orders a block device using the maximum IOPS for the given size
    * authorizes the worker node to use the block device
    * attaches the block device to the worker node
    * creates a PV for the block device
   

API Endpoint:  
**POST /api/v1/createBlockClassic/**  

Example Payload

```
{ "apikey": "",
  "cluster_name": "",
  "size": "",
  "pv_name": ""
} 
```
**apikey:** apikey of your IBM Cloud Account where your ROKS cluster is located

**cluster_name:** name of your ROKS cluster

**size:** Size of the block device to create in GB

**pv_name:** Name of the persistent volume to create

			
example usage:

	curl -X POST -H "Content-Type: application/json" 'api.ibmcloudhelper.com:8000/api/v1/createBlockClassic/' -d '{"apikey": "", "cluster_name": "", "size": "", "pv_name": "" }'
	
## Utility

### Check if ROKS Cluster is ready
Checks a ROKS cluster to see if the ingress subdomain has been set for the cluster and the cluster details populate the resource group name.  After the cluster is provisioned, it can take up to 30 minutes for the cluster to recognized the resource group name it was create it. 

API Endpoint:  
**POST /api/v1/checkClusterReady/**  

Example Payload

```
{ "apikey": "",
  "cluster_name": ""
} 
```
**apikey:** apikey of your IBM Cloud Account where your ROKS cluster is located

**cluster_name:** name of your ROKS cluster

example usage:

	curl -X POST -H "Content-Type: application/json" 'api.ibmcloudhelper.com:8000/api/v1/checkClusterReady/' -d '{"apikey": "", "cluster_name": ""}'

## OpenShift

### Get ROKS Verions	
Using a local redis cache, this api quickly returns a list of versions available in ROKS.

API Endpoint:  
**POST /api/v1/getROKSVersions/**  

example usage:

	curl -X POST -H "Content-Type: application/json" 'api.ibmcloudhelper.com:8000/api/v1/getROKSVersions/'

### Get ROKS Token	
Retrieves an ROKS token and login command by providing your apikey and clustername.

API Endpoint:  
**POST /api/v1/getROKSToken/**  

example usage:

	curl -X POST -H "Content-Type: application/json" 'api.ibmcloudhelper.com:8000/api/v1/getROKSToken/' -d '{"apikey": "", "cluster_name": "" }'