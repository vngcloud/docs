# Containers naming rule

#### Rule for naming a container <a href="#containersnamingrule-rulefornamingacontainer" id="containersnamingrule-rulefornamingacontainer"></a>

* The container name must be between 3 (minimum) and 235 (maximum) characters long.
* The container name can only include uppercase and lowercase letters (a-z, A-Z), numbers (0-9), periods (.), spaces ( ), underscores (\_), hyphens (-), and the @ symbol.
* The container name should not contain sensitive information (e.g., IP addresses, account names, login passwords, etc.). We recommend using lowercase letters, numbers, and avoiding specific characters such as #, @, $, %, ?, /, \`, \~, etc. If you really need to use uppercase letters, please note that you may encounter issues when working with supported third-party software from different providers.
* The container name must be unique within a project until the container is deleted.

#### Examples <a href="#containersnamingrule-examples" id="containersnamingrule-examples"></a>

* The following examples of container names below are valid and adhere to the suggested naming principles:\

  * containerexample1
  * container-data-2022
  * ...
* The following examples of container names are valid but not recommended for use:\

  * [docexamplewebsite.com](http://docexamplewebsite.com/)
  * [www.docexamplewebsite.com](http://www.docexamplewebsite.com/)
  * ...
* The following examples of container names are invalid:\

  * Container data đạt hiệu quả 80 % (chứa ký tự %)
  * con\_1/2022 (chứa ký tự /)
  * ...
