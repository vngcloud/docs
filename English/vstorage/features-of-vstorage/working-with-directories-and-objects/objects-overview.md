# Objects overview

You can start working with vStorage by interacting with projects, containers, and objects. A container serves as a storage space for objects. An object is the fundamental storage entity that holds both the original data and metadata information of a file uploaded to the vStorage system.

To store an object in vStorage, you create a container and then upload a file to that container. The newly uploaded file is stored within the container as an object. Once an object is in a container, you can perform various operations such as uploading another file to overwrite the object (updating the object), downloading, copying, moving, or modifying tag and metadata settings for that object. When you no longer need an object or a group of objects, you can delete them to clean up your resources on vStorage.

An object in a container includes the following information:

* **General Information**: Name, size, content type, path to the object.
* **Tag**: A label attached to an object for identification, classification, or providing additional related information.
* **Metadata**: Information about the data, including details such as name, address, size, creation date, and other attributes. It can be used to help users understand and access the desired data better.
* **Checksum**: A string of numbers and letters obtained through a computation process from the original data and metadata of a file. It is used to detect errors that may occur during transmission or storage. Checksums are commonly used to verify the integrity of data but are not relied upon to verify the authenticity of the data.
* **Version**: A term used to refer to a version of software or documentation. Versions are used in the context of versioning features.
