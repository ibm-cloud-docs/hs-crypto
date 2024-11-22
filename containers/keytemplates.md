# Key templates

All keys created in {{site.data.keyword.uko_short}} must be created through a key template. Key templates comprise a set of properties that define the key algorithm, key label template, key length, initial state, and so on. It also defines the context the keys will be used in and certain values are therefore predefined.

You access key templates through the **Key Management** &gt; **Key templates** menu.

When creating a key template the field Key application is prefilled with `Pervasive Encryption`. In future releases more key template applications will be supported.

Depending on the setting on the key template, keys can be created in either `ACTIVE` or `PRE-ACTIVATION` states. When a key is created in `PRE-ACTIVATION` state, it is not distributed to keystores, it must be activated to be distributed. When a key is created in `ACTIVE` state, or a `PRE-ACTIVATION` key is activated, the key is distributed to all keystores defined in the key template.
{: note}

The binding between a key and its key template must remain intact. For this reason, you can never use {{site.data.keyword.uko_short}} or {{site.data.keyword.uko_short}} to delete a key template that has been used for key generation. You can however `Archive` a key template to prevent it from being used for generation of new keys.

Key templates that are defined in {{site.data.keyword.uko_short}} are fully supported on the {{site.data.keyword.uko_short}}.

Among the key templates that are defined in {{site.data.keyword.uko_short}}, only a template with these traits is supported by {{site.data.keyword.uko_short}}:

* It has an instance in any Zone other than `2` (internal {{site.data.keyword.uko_short}} repository)

* The system management list contains the value `WEB`

## Key label templates

When a key template generates a key, the key label is created based on the definition in the template. Your key label template can provide text fields and `tags` that a user can modify upon key generation. Those tags are called `custom tags` in {{site.data.keyword.uko_short}} and {{site.data.keyword.uko_short}}.

Use key label templates to define and maintain naming conventions for keys. For example, your key template could apply a prefix for the environment and a suffix for the application name to all application keys, as follows:


```
&lt;ENVIRONMENT&gt;.AES.DATA.&lt;APP_NAME&gt;
```

where:

* `&lt;ENVIRONMENT&gt;` represents a high-level qualifier for environment, for example, `TEST` or `PROD`
* `&lt;APP_NAME&gt;` represents the name of the application, for example, `WAS` or `MQ`

A `custom tag` is defined by wrapping a name within less-than (`&lt;`) and greater-than (`&gt;`) symbols, as in this example: `&lt;ENVIRONMENT&gt;`. 
{: note}
