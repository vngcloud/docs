# Image Management

Access a Repository to manage the images stored within it using the following features:

#### View Image List

On the Image list page, users can view the list of Images along with the following information:

* **Image Name:**\
  The name of the image.
*   **Artifact:**\
    The total number of Artifacts associated with the Image.

    **More about Artifacts:**\
    When pushing an image that already exists in the Repository, if the Image contains significant changes (for example, changes in layers), the system will automatically create a new Artifact corresponding to the newly pushed Image while keeping the same Image name.
* **Pull Count:**\
  The total number of pulls for the Image.
* **Last Modified At:**\
  The most recent pull/push activity associated with the Image.

***

### View Image Details

On the Image detail page, users can view the list of Artifacts associated with the Image along with the following information:

* **Artifacts:**\
  The corresponding Artifact ID.
* **Tag:**\
  The list of tags associated with an Artifact.
* **Size:**\
  The image size corresponding to each Artifact.
* **Push Time:**\
  The most recent push time (recorded when there are changes to image tags/artifacts).
* **Pull Time:**\
  The most recent pull time for the Artifact.

***

### Push an Image

#### How to Push an Image to a Repository

1. Open Docker/Podman and log in using a Repository User that has **Push** permission on the target Repository.
   * **Username:** Repository Name
   * **Password:** Repository User Secret Key
2. Access the vCR Console and select the Repository where you want to upload the image. In the **"Image"** tab, click **"Push Command"** to quickly view the required commands.
3. Copy the **"Tag an image for this project"** command to tag the image before pushing.
4. Copy the **"Push an image to this project"** command to push the image to the Repository.
5. Verify that the image has been successfully pushed by checking the **"Image"** tab on the Repository detail page.

***

### Pull an Image

#### How to Pull an Image from a Repository

1. Open Docker/Podman and log in using a Repository User that has **Pull** permission on the Repository storing the image.
   * **Username:** Repository Name
   * **Password:** Repository User Secret Key
2. Access the vCR Console and select the Repository containing the image you want to download. In the **"Image"** tab, open the detailed Image page.
3. On the Image detail page, in the **"Action"** column, click the **three-dot icon** next to the Image Artifact you want to download.
4. A **"Copy Pull Command"** popup will appear, allowing users to quickly copy the appropriate pull commands:
   * **Pull by Artifact:**\
     Pulls the Image Artifact with the latest tag by default.
   * **Pull by Artifact Tag:**\
     Pulls the Image Artifact using a specific tag.
