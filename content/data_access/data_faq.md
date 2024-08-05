Frequent Ask Question
===

## How to Access the Regional MOM6 Data?
Currently, the regional MOM6 output can be accessed through the PSL THREDDS server. Users have the flexibility to choose their preferred method of data retrieval from this server. Additionally, an alternative option involving AWS cloud storage is under consideration and may become available in the near future. This option is currently undergoing testing. For direct access to the THREDDS server, [go to the catalog directly](https://psl.noaa.gov/thredds/catalog/Projects/CEFI/regional_mom6/catalog.html).

To access/download the data, the [CEFI portal model data access](https://psl.noaa.gov/cefi_portal/#data_access) offer couple different options.
- A list of available variable tables in different coastal regions is provided in multiple format (html, json, and xml)
- A data query generator to generate code to access the data through OPeNDAP
- A data query generator to provide direct download
Once the AWS cloud storage is available, the data query generator will also include the related options.

## What is OPeNDAP and THREDDS Server?
**OPeNDAP :**
OPeNDAP stands for "Open-source Project for a Network Data Access Protocol". It's a free, open-source software that allows scientists to share data more easily over the internet. It works like a translator for a wide variety of data formats and types. This means that data stored in different formats can be accessed in a uniform way. It's used by many organizations, including NASA and NOAA, for providing access to Earth science data.

**THREDDS Server:**
THREDDS stands for "Thematic Real-time Environmental Distributed Data Services". It's a web server that provides metadata and data access for scientific datasets. It uses a variety of remote data access protocols, including OPeNDAP. This means that THREDDS can use OPeNDAP to provide data access. THREDDS also provides catalog services that list datasets and the data access services available for the datasets.

**The Relation:**
So, in simple terms, OPeNDAP is a protocol (a set of rules) for accessing and sharing data over the internet, and THREDDS is a server that can use this protocol (among others) to provide access to scientific datasets. This means that a THREDDS server can serve data using the OPeNDAP protocol. In other words, OPeNDAP is one of the tools that THREDDS uses to do its job.

## What is AWS Cloud Storage
**Amazon Web Services (AWS) Cloud Storage**, also known as **Amazon Simple Storage Service (Amazon S3)**, is an object storage service provided by Amazon Web Services. It utilizes object storage architecture to offer global accessibility through HTTP requests or an Application Programming Interface (API).
In the realm of object storage, each "object" represents a distinct unit stored in a "storage pool". Unlike hierarchical storage systems commonly used in operating systems, which have folders, subfolders, and files, a storage pool is flat. All objects are stored at the same level within it.
“Bucket” is used to group similar “objects” together for organization purposes. However, it’s important to note that there is no hierarchical relationship between a bucket and its objects.
Each object in the storage pool carries three essential components: a unique identifier, metadata, and the data itself. This structure allows for unlimited scalability, a key advantage of object storage.
Object storage is particularly suitable for static and unstructured data. For instance, in the case of model simulations, the output is structured and becomes static once generated. The scalability of object storage is crucial for handling these simulations, especially as they grow with time to petabyte scale and more.
This option is currently undergoing testing and not allow public access yet.

