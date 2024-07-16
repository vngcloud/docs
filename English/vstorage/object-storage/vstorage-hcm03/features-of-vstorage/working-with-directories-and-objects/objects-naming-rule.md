# Objects naming rule

#### Rules for renaming objects <a href="#objectsnamingrule-rulesforrenamingobjects" id="objectsnamingrule-rulesforrenamingobjects"></a>

The following rules apply to renaming objects in vStorage:

* **Length**: The object name must be between 1 (minimum) and 255 (maximum) characters long.
* **Allowed characters**: The object name can include uppercase and lowercase letters (a-z, A-Z), numbers (0-9), all special characters, and spaces if needed.
* **Restriction on special characters**: To minimize errors when working with objects using user-side tools or on vStorage, we recommend avoiding special characters such as $, #, %, &, ^, etc., in object names. It is advisable to use the Latin alphabet for naming objects and directories.

#### Regulations on the maximum file size when uploading: <a href="#objectsnamingrule-regulationsonthemaximumfilesizewhenuploading" id="objectsnamingrule-regulationsonthemaximumfilesizewhenuploading"></a>

* There is no limit on the number of files in a single upload or download.
* The maximum total file size for files uploaded through the vStorage Portal in a single upload is 20GB.
* The maximum total file size for files uploaded through 3rd party software or the vStorage API in a single upload is 5TB.
