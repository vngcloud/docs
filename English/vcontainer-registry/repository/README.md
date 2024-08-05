# Repository

## What is a Repository?

A Repository is a central location where Docker images are stored and managed. It acts as a storage space for different versions (versions) of images, each identified by a unique tag. Depending on the access control settings, this Repository can be public (accessible to everyone) or private (accessible only to authorized users).

## What Can I Do with Repositories?

**CREATE A REPOSITORY**

To create a Repository, click on the "Create a repository" button. You will then be asked to fill in the necessary information such as Repository name, Access level (public or private), and Quota Limit (maximum storage capacity). For more details, refer to the "Create Repository" section.

**EDIT QUOTA LIMIT**

To adjust the storage limit of a Repository, first, go to the Repository list screen and locate the "Action" column. Click on the "three dots" icon on each Repository row in the "Action" column and select "Edit Quota Limit". For more information, refer to the "Edit Quota Limit" section.

**IMAGE MANAGEMENT**

Access the Repository and click on the "Images" tab to view the list of images currently stored in the Repository. Then, click on a specific image to view its details (artifacts and tags) and copy the push/pull commands for the related artifacts/tags. For more details, refer to the "Image Management" section.

**REPOSITORY USER MANAGEMENT**

View the list of attached Repository Users by clicking on the "Repository User" tab on the Repository details page. From here, you can quickly create, attach, or detach a Repository User.

* In a private Repository, Repository Users can push (upload) and pull (download) container images, ensuring secure access to the images managed in the Repository.

For more details, refer to the "Repository User" section.

**VIEW HISTORY**

The access history of the Repository allows you to track all actions related to it, including actions on the Repository itself and related Images. For more information, refer to the "Repository History" section.
