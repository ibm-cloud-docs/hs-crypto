# Rotating recovery key and KEK

1. To rotate the recovery key, first import the new recovery key into the keystore, e.g. via TKE .
1. Navigate via the menu to **Administration** 
2. Specify a new key label for 
    * `{{site.data.keyword.uko_short}} recovery key label (AES)`
    * `AES DATA keys KEK label (RSA)`
    * `AES CIPHER keys KEK label (AES)`
1. Save changes after each individual update. 

From now on, all new keys generated with any key template _in the default vault_ in {{site.data.keyword.uko_short}} will use the new KEKs that are protected with the new recovery key. 

To verify that the new recovery key (e.g. `TZMKAES.KEYMNGNT.ZONEICSF.KEK00002`) is used to protect the updated KEKs, you could run an SQL query against the database which will return all KEKs that are still protected by the old recovery key.

```
select *
from EKMF_WEB_KEYS
where KEY_TEMPLATE_NUMBER in ('AES-W011', 'RSA-W050')
  and KEK_LABEL <> 'TZMKAES.KEYMNGNT.ZONEICSF.KEK00002'
```

