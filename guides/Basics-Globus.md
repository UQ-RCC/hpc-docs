Globus Markdown

# The Globus Basics

>[!Note]
>
>This page is still under construction

## What is Globus ?

Globus is ...

## What are the limitations and risks ?

Currently, our UQ Globus endpoint does not support encrypted transfers. UQ RCC are addressing this.
All data transferred into/out of UQ Globus endpoint is *NOT* encrypted.

## How to get an RDM "Q" storage allocation connected to UQ Globus Service ?

There is a process we will walk you through. Please email rcc-support@uq.edu.au to have your Q storage allocation connected to Globus. Note that you must be the owner of the RDM storage collection record that contains the "Q" data storage allocation. 

## Basic Globus Usage

### Overview

The Globus web interface is the primary method of access.
It allows you to move files and folders between sites.
It also allows you to download files to your local computer (or a network drive attached to that local computer)

### Registering to use Globus

Anyone with a AAF, ORCID, GitHub or Google account credential can apply for access to an endpoint. Most Australian higher education sector people should use their AAF credential.

We will do that automatically as part of the process of connecting your RDM collection to the Globus endpoint. 

If you are connecting to globus to pull data from a collaborator's Globus endpoint to your local machine, and you won't have your RDM storage allocation connected directly to Globus, then you will need to be manually registered to access the Globus endpoint. Again, an email to rcc-support@uq.edu.au will sort that out.

### Getting at the UQ endpoint

Visit https://app.globus.org/endpoints

Login with your institutional credentials

If you don't land in the UQ endpoint automatically, search for "The University of Queensland"

An individual can have multiple institutional credentials but they will have to be linked to the same GlobusID. For example if you have joined UQ (welcome!) and still have access to your previous institution and need to pull your data to UQ, then you will have a single GlobusID but it will be associated with the multiple institution identifiers.

### Globus Connect Personal Software

Globus provides a desktop tool that enables your personal computer to pretend to be a Globus endpoint.
There is a link to the "Get Globus Connect Personal" on the Collections part of the Globus web interface.

You might find the Personal Connect software useful if you are sending or receiving data from your workstation. </br>
You will find it necessary to use the Globus Connect Personal application to _transfer_ big files (>1GB) to the destination.

You do not need Globus Connect Personal to move data between, say, UQ Globus endpoint and a remote endpoint. Just use the app.globus.org website.  

### Finding your data

Globus uses the term Collection for a group of folders containing data that may belong to different groups.

On the UQ endpoint you need to 

* click on COLLECTIONS (you see a list that includes "QRIScloud Data" and you should be subscribed to that Globus Collection if you requested your RDM storage allocation be connected.)
* click on the ">" link which will show "collection details"
* click on the "Open in File Manager" button  </br>

Alternatively, you can 
* click on the FILE MANAGER icon in the left panel 
* type QRIScloud Data into the search field
* click on the folder that belongs to you from the long list
 


### Not working?

There are a few things we've noticed that can go wrong in your Globus session.

* Too soon, maybe? </br>
There is a process that is only run once every 24 hours, in the middle of the night, that is required before an RDM Storage Allocation becomes accessible in Globus File Manager (even if it is visible in the list of collections)

* Blank panes? </br>
Sometimes the web interface does not display the list of Collections, or the folders in a Globus Collection. Hit page reload button in your browser, that usually fixes it.

* Sometimes you might get authentication or access errors. You may need to logout and login again.

* Sometimes you are trying to access a Q collection and will get "Authentication/Consent is required for Globus transfer service to manage data on this collection." errors. Click on the Continue button. You will be offered a blue URL click on the link that looks like your **username@institution.dommain.name** Do not use the drop down menu of Institutions because it gets stuck in an infinite loop!

* It is not possible to use the Upload file feature with files in excess of 1GB. Use the Globus Connect Personal application to _transfer_ big files to the destination.
* If all else fails, email rcc-support@uq.edu.au
