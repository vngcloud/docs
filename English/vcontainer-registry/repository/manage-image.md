# Manage image

You can access the Repository to manage images with the following features:

## Viewing the Image List

On the Image list screen, you can view the list of Images with information such as:

* **Image name:** The name of the image.
* **Artifact:** The total number of Artifacts corresponding to the Image.
  * **Explanation of Artifact:** When uploading the same image already in the Repository, if the Image has major changes (such as layer changes), a new Artifact will be automatically generated corresponding to the newly pushed Image with the same Image name as before.
* **Pull Count:** The total number of Pulls for the Image.
* **Last Modified At:** The last time a Pull/Push was performed, calculated for the Image.

## Viewing Image Details

On the Image details screen, you can view the list of Artifacts of the Image with information such as:

* **Artifacts:** The corresponding ArtifactId.
* **Tag:** The list of tags corresponding to one Artifact.
* **Size:** The size of the image corresponding to each Artifact.
* **Push Time:** The last push time (recorded when there is a change in the image tag/artifact).
* **Pull Time:** The last pull time (calculated for the Artifact).

## Pushing (Uploading) an Image

**How to push an image to store in the Repository**

1. Open docker/podman and log in with a Repository User who has Push permission on the Repository where the image will be stored:

* **User name:** Repository Name
* **Password:** Repository User Secret Key

2. Access the vCR Console, click on the Repository you want to upload the image to, in the "Image" tab, click on "Push Command" to quickly view the necessary commands.
3. Copy the command "Tag an image for this project" to tag the image you want to push.
4. Copy the command "Push an image to this project" to push the image to the Repository.
5. Check if the image has been successfully pushed in the "Image" tab on the Repository details page.

## Pulling (Downloading) an Image

**How to pull an image from the Repository**

1. Open docker/podman and log in with a Repository User who has Pull permission on the Repository storing the image:

* **User name:** Repository Name
* **Password:** Repository User Secret Key

2. Access the vCR Console, click on the Repository storing the image you want to download, in the "Image" tab, access the Image details you want to download.
3. On the Image details screen, in the Action column, click on the "three dots" icon next to the Image Artifact you want to download.
4. A "Copy pull command" popup will appear, allowing you to quickly copy the corresponding pull commands:

* **Pull by Artifact:** By default, download the Image Artifact with the latest tag.
* **Pull by specific Artifact tag:** Pull the Image Artifact with each specific tag.
