
# FileOpen PodViewer for ESS 

## What does it do?
This is an integration of the FileOpen controlled document viewer with Inrupt's Enterprise Solid Server (ESS) and PodBrowser. The system encrypts and then selectively decrypts PDFs after obtaining identity and permission data from ESS.

The app extends the functionality of PodBrowser's Sharing control to the viewing environment of the document. 

With PDFs PodBrowser controls only initial access: once a PDF has been extracted from the Pod it is no longer managed[^1].

FileOpen PodViewer implements a controlled display environment for PDFs, restricting access to only the WebIDs that were specified in PodBrowser and preventing further distribution. Changing the access rules in the Pod also changes the access to the PDF, i.e. access can be restricted or revoked at any time.

The viewing environment can also be used with fewer or no access restrictions, or with additional security to provide more fine-grained control over printing, text extraction, annotation and other features. All actions can be logged.

## How does it work?
PodBrowser supports three classes of restriction for viewing files:  
* Anyone 
* Anyone signed-in
* A specific WebID

The system supports each of these cases. It operates by presenting a login-page and signing the user into PodBrowser via Solid-OIDC, then evaluating that user's identity against the restrictions in the Pod for that Document.

Once the user's identity has been established and validated against the PodBrowser's access control rules the PDF is then rendered by the FileOpen viewer system. This process involves a number of steps:

* Real-time delivery of a PDF viewer into the user's browser and then of the encrypted PDF into that environment.
* Interaction from within the browser with a secondary server (the _PermissionServer_) to obtain the decryption key for that PDF and a set of rules governing access. 
* Client-side decryption and rendering of the PDF, with user/document specific watermarking and dynamic control over UI and usage.

This approach prevents capture of a usable PDF from the communication channel or the browser-context and ensures that each document-open event is under the control of the Pod owner. 
The FileOpen Viewer system also supports a variety of fine-grained controls over expiration, concurrent usage, watermarking, etc.


## Limitations of this Implementation:

* In this version the encryption of the PDF itself is done outside of the demo, i.e. prior to the PDF being uploaded to PodBrowser. In a fully developed system the ability to encrypt PDFs would be exposed from within the PodBrowser interface or via a separate upload utility.
* This version renders all PDFs as read-only documents without the option to download. In a complete system the document owner would be given control over the end-user experience, i.e. could enable editing, downloading, etc.


https://user-images.githubusercontent.com/19676307/236293950-58798d34-4ae1-44e5-96f2-2f7813252328.mp4


## Video Explanation



# Video with CC Link

https://www.dropbox.com/s/6wj5v1dz79x3h4y/FileOpen%20PodViewer.mp4?dl=0

[^1]: We recognize that Solid in general and PodBrowser in particular are not designed to control objects once extracted (cf the prescient comment from timbl [in this thread](https://forum.solidproject.org/t/can-i-restrict-where-users-data-can-go/5555/4)), but nevertheless believe that there are important use cases, especially in regulated industries, for post-distribution control and usage tracking within the Inrupt ESS ecosystem.



