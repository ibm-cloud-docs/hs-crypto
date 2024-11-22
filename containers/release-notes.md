# Release Notes 

Versions of {{site.data.keyword.uko_short}} released

**Version 1.3.1**

New features:

-   Support for `Install in keystores` flag from EKMF WS key templates

-   Major improvements to the Audit log view showing more information

Fixes:

-   `Created on` is not updated on key or key template updates

-   Destroying a key removes its key value from the repository

-   Destroying a key is only possible if it's uninstalled from all keystores

**Version 1.3.0**

New features:

-   Introduces support for Amazon Web Services Key Management Service (AWS KMS) keystores

-   Keys can be generated based on an existing key

-   Key list filtering improvements

-   Key labels set in the settings view are validated against ICSF key label rules

-   Dataset view search and filtering improvements

-   Adds a new view for keystore type selection before defining it

-   Adds logos to keystore cards to identify keystore type at glance

-   Adds cancel button to keystore and key template editing views

-   Key templates can be copied to create new key templates

-   Key templates can be archived

-   Key template list can be viewed in a table in addition to card view

-   Key template list table can be sorted

-   Key template and keystore definition views can be saved with keyboard shortcut CMD/CTRL+S

-   Key template can be previewed by clicking on a key template card

-   Archived key templates can be edited

-   Adds a `Generate key` button in the key template table view

-   Adds key label of the KEK on key details view

-   Key state change can be done on multiple selected keys

-   A description can be added to a key upon generation (default taken from a key template)

-   Authentication improvements

Fixes:

-   Audit log table display fixes

-   Imported key templates will always be set to active

-   Key template form autofocus fixes

-   Better error handling on key generation wizard view

-   Keystore status reporting fixes

-   Shows key template description in the key generation view

-   Keeps search results after changing key status in the key list view

-   Disallows `seqno` as the first tag in key label template as a key label cannot begin with a digit

-   Editing existing key template's key label no longer resets the cursor to the end of line during edit

-   Port number fields will no longer accept negative numbers

-   Prevents text overflow in toast notifications

-   Removes the generate key option from the template of key template overflow menu if is archived

-   Information about key template state is read only

-   Editing archived template and saving it now activates the key template

-   List of keystores associated with a key template is always shown at the key generation view

-   All input in the settings view is auto-capitalized

-   Breadcrumbs adjustments

-   Notification framework fixes

-   Accessibility fixes

-   Performance improvements

**Version 1.2.2**

Fixes:

-   Updated web.xml to remove static definitions of web listeners

-   Added an automatic migration that assigns keystores to existing key templates

**Version 1.2.1**

New features:

-   Added EKMF Workstation key templates

Fixes:

-   Added missing keystore table definitions

**Version 1.2.0**

New features:

-   Support for all states from the NIST key state model

-   Key templates can be archived

-   Filter key template list by name

-   Filter key template list by state

-   Keys can be sorted

-   Key template defines which keystores to distribute keys to

-   Key generation view shows which keystores will receive the key

Fixes:

-   Audit log data is aligned with EKMF WS

-   Changing key state no longer clears search results

-   Searching handles wildcards in a more intuitive manner

**Version 1.1.0**

New features:

-   Import/export key templates

-   View audit log

-   Removal of key from key store

-   AES 256-bit CIPHER keys protected by a 256-bit AES hierarchy

-   NIST key state model; PRE-ACTIVATION, ACTIVE, and DEACTIVATED states

-   Key activation and deactivation

-   Filter keys by state

-   Filter keys by key label

-   Sequence number tag for automatic numbering of keys

**Version 1.0.0**

New features:

-   Generate AES data keys for pervasive encryption

-   Create, import and export key templates

-   Data set analysis view
