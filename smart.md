# SMART

## USB Bridge

Specify the device type with `-d`
when the system is not able to detect it automatically.

```bash
smartctl -d sat -a /dev/sdf
smartctl -d sat -t short /dev/sdf
```

## Fails

> Attributes  are  one  of  two  possible
> types:  Pre-failure or Old age.  Pre-failure Attributes are ones
> which, if less than or equal to their threshold values, indicate
> pending  disk  failure.   Old age, or usage Attributes, are ones
> which indicate end-of-product life from old-age or normal  aging
> and wearout, if the Attribute value is less than or equal to the
> threshold.  Please note: the fact that an Attribute is  of  type
> 'Pre-fail'  does  not  mean that your disk is about to fail!  It
> only has this meaning  if  the  Attribute´s  current  Normalized
> value is less than or equal to the threshold value.
