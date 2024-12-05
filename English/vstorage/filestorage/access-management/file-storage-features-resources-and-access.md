# File Storage features, resources, and access

**File Storage resources supported for access authorization:**

* File Storage

***

**File Storage feature and permissions needed to implement the feature:**

We provide you with 3 main permission groups (List, Read, Write) with meanings described in the table below:

<table data-full-width="true"><thead><tr><th width="215">Action</th><th width="477">Description</th><th>Resource</th></tr></thead><tbody><tr><td>ListFileStorage</td><td>Get list of storage files</td><td>N/A</td></tr><tr><td>ListTag</td><td>Get list of tags on each storage file</td><td><ul><li>All resources or by specific file-storage-id resource</li></ul></td></tr><tr><td>GetFileStorage</td><td>Get details of a storage file</td><td><ul><li>All resources or by specific file-storage-id resource</li></ul></td></tr><tr><td>GetMountGuide</td><td>Get mount target information</td><td><ul><li>All resources or by specific file-storage-id resource</li></ul></td></tr><tr><td>CreateFileStorage</td><td>Create a new file storage</td><td>N/A</td></tr><tr><td>CreateFileStorageTag</td><td>Create a new tag for file storage</td><td><ul><li>All resources or by specific file-storage-id resource</li></ul></td></tr><tr><td>ResizeFileStorage</td><td>Change the max quota size of a Storage File</td><td><ul><li>All resources or by specific file-storage-id resource</li></ul></td></tr><tr><td>EditFileStorage</td><td>Edit a storage file</td><td><ul><li>All resources or by specific file-storage-id resource</li></ul></td></tr><tr><td>EditFileStorageTag</td><td>Edit the tags of a storage file</td><td><ul><li>All resources or by specific file-storage-id resource</li></ul></td></tr><tr><td>DeleteFileStorage</td><td>Delete a storage file</td><td><ul><li>All resources or by specific file-storage-id resource</li></ul></td></tr><tr><td>DeleteFileStorageTag</td><td>Remove tags from a storage file</td><td><ul><li>All resources or by specific file-storage-id resource</li></ul></td></tr></tbody></table>
