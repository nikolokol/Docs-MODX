---
title: "toJSON"
_old_id: "1218"
_old_uri: "2.x/class-reference/xpdoobject/field-accessors/tojson"
---

## xPDOObject::toJSON()

Returns a JSON representation of the object.

## Syntax

API Docs: <http://api.modxcms.com/xpdo/om/xPDOObject.html#toJSON>

``` php 
string toJSON (
   [string $keyPrefix = ''],
   [boolean $rawValues = false]
)
```

## Example

``` php 
$object->set('name','Bob');
$object->set('email','pinkdaisies@gmail.com');
$json = $object->toJSON();
echo $json;
// prints {"name":"Bob","email":"pinkdaisies@gmail.com"}
```

## See Also

- [fromArray](xpdo/class-reference/xpdoobject/field-accessors/fromarray "fromArray")
- [toArray](xpdo/class-reference/xpdoobject/field-accessors/toarray "toArray")
- [fromJSON](xpdo/class-reference/xpdoobject/field-accessors/fromjson "fromJSON")
- [toJSON](xpdo/class-reference/xpdoobject/field-accessors/tojson "toJSON")