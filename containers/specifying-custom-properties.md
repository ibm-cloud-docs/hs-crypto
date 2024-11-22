# Specifying custom properties

When [creating a key template](uko-create-template-onprem.md) for Pervasive Encryption (keystore type KMG), you can scroll to the very bottom of the page to open 'Advanced Properties' (optional), where you can enter the following custom properties that will affect the created keys.

## CCA Keywords

When creating AES keys for Pervasive Encryption, they are fine-tuned to that use-case. If you need to generate AES keys for other purposes (e.g. to use with GKLM), you can overwrite the default keywords that are used to generate the `CIPHER` keys.

### Example 1

If you need to generate a key that supports AES GCM mode but do not allow for it to be used by CPACF, you can specify advanced properties this way:
```json
{
  "keystores": [
    {
      "cca_key_words": [
        "DECRYPT",
        "ENCRYPT",
        "V1PYLD",
        "ANY-MODE",
        "XPRT-SYM",
        "NOEX-RAW",
        "NOEXUASY",
        "NOEXAASY",
        "NOEX-DES",
        "XPRT-AES",
        "NOEX-RSA"
      ]
    }
  ]
}
```
{: codeblock}


## Naming Scheme (optional)

The naming scheme is generally controlled by the UI, see [Defining key naming schemes](uko-create-template-onprem.md#define-naming-scheme). This defines the main naming scheme in the {{site.data.keyword.uko_short}} repository, and since [fixpack 3.1.0.1](whats-new.md#whats-new-3101) also in keystores using key instance naming schemes. 

**Note:** After Fixpack 3.1.0.1 it is not required anymore to define key instance naming schemes using advanced properties, because it can be done in the UI. 

Key instance naming schemes can be defined using the Advanced Properties as shown in the following example:

### Example 2

Naming scheme defined in the UI: `<h>.KMGAES.PE<APP>`.

Advanced properties:
```json
{
  "keystores": [
    {
      "naming_scheme": "<h>.KMGAES.PE<APP><seqno>"
    }
  ]
}
```
{: codeblock}

When defined this way, performing a [key rotation](uko-rotate-key-onprem.md) on [keys](uko-intro-keys-onprem.md) created with this [key template](uko-intro-templates.md) will create keys whose labels in keystore are (for `h=J` and `APP=DEMO`):

1. `J.KMGAES.PEDEMO00001`
1. `J.KMGAES.PEDEMO00002`
1. `J.KMGAES.PEDEMO00003`

etc.

### Example 3

Naming scheme defined in the UI: `<h>.KMGAES.PE<APP>`.

Advanced properties:
```json
{
  "keystores": [
    {
      "naming_scheme": "<h>.KMGAES.PE<yy><mm>.<APP>"
    }
  ]
}
```
{: codeblock}

When defined this way, performing a [key rotation](uko-rotate-key-onprem.md) on [keys](uko-intro-keys.md) created with this [key template](uko-intro-templates.md) will create keys whose labels in keystore are (for `h=J` and `APP=DEMO`):

1. `J.KMGAES.PE2308.DEMO` when the key is generated in August of 2023.
1. `J.KMGAES.PE2402.DEMO` when the key is rotated in February of 2024.
1. `J.KMGAES.PE2408.DEMO` when the key is rotated in August of 2024.

etc.


You can use [system placeholders](uko-create-template-onprem.md#create-template-system-placeholders) in addition to any placeholders used on the key entry in the {{site.data.keyword.uko_short}} repository.


## Combining properties

### Example 4

Those properties can be used together, i.e. you can specify advanced properties like this:
```json
{
  "keystores": [
    {
      "naming_scheme": "<h>.KMGAES.PE<yy><mm>.<APP>",
      "cca_key_words": [
        "DECRYPT",
        "ENCRYPT",
        "V1PYLD",
        "ANY-MODE",
        "XPRT-SYM",
        "NOEX-RAW",
        "NOEXUASY",
        "NOEXAASY",
        "NOEX-DES",
        "XPRT-AES",
        "NOEX-RSA"
      ]
    }
  ]
}
```
{: codeblock}

### Example 5
You do not need to format the field with indentation, but it needs to be in JSON format, and needs to conform to the API spec.

```json
{ "keystores": [ { 
  "naming_scheme": "<h>.KMGAES.PE<lay><lam>.<APP>", 
  "cca_key_words": [ "DECRYPT", "ENCRYPT", "V1PYLD", "ANY-MODE", "XPRT-SYM", "NOEX-RAW", "NOEXUASY", "NOEXAASY", "NOEX-DES", "XPRT-AES", "NOEX-RSA" ]
   } ] }
```
{: codeblock}
