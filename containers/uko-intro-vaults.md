# Vaults

This section contains the following chapters: 
* To find out how to create a vault, check out [Creating vaults](uko-create-vaults-onprem.md)
* To find out instructions on editing a vault, check out [Editing vaults](uko-edit-vaults-onprem.md)
* To find out how to delete a vault, check out [Deleting vaults](uko-delete-vaults-onprem.md)

Vault, comparing to the previous version, 2.1, is a new object type. It is located on the top of the hierarchy containing keys, key templates or keystore connections. Each key, key template or keystore connection can only belong to a single vault and cannot be shared across vaults. 

Keys in vaults could be secured either on the system or vault level. This allows to have vault specific security keys to protect data in case of a disaster, or lost backups. More about it is described in [Creating vaults](uko-create-vaults-onprem.md).

By default, the system contains a default vault with the ID of `00000000-0000-0000-0000-000000000000` that cannot be removed. If you are migrating from version 2.1, all existing keys, key templates and keystore connections will be placed in the default vault. 


