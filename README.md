# SimpleJSON
A simple one class file to parse, modify, and export JSON.

## SimpleJSONUnity
A one class extension to SimpleJSON that allows parsing, modifying, and exporting of common Unity objects (`Vector2`, `Vector3`, `Quaternion`, `Rect`, `Color`, etc.)

## SimpleJSONBinary
A one class extension to SimpleJSON that provides methods to serialize a JSON object tree into a compact binary format.

# Disclaimer
This forked version of Bunny83's SimpleJSON contains modifications that I've made for another project, [ChroMapper](https://github.com/Caeden117/ChroMapper). The changes are listed below.

## Changes from `Bunny83/SimpleJSON`
- Added `JSONParseException` which SimpleJSON throws instead of a generic `Exception` when calling `JSON.Parse` or `JSONNode.Parse`.
  - It includes `TokenLocation`, which is a string to the location where the parsing has failed
    - For example: `_customData._preciseSpeed`
  - It also includes `ToUIFriendlyString()`, which [I mainly use for outputting to the user when using ChroMapper](https://cdn.discordapp.com/attachments/702231982335197264/729070283092394036/unknown.png).
- SimpleJSON now throws a `JSONParseException` when a new node starts being parsed before an existing node is completed.
  - Works on both new lines and on a single line.
  - For example, trying to parse `{ "_objectA": "someValue" "_objectB": "someOtherValue" }` will throw a `JSONParseException`, whereas in the original SimpleJSON, the returned JSONNode will exclude `_objectB`.
- Added support for Color in `SimpleJSONUnity`
  - Supports both Array format (`[r, g, b]`) and Object format (`{ "r": r, "g": g, "b": b }`)
    - Alpha is optional, and defaults to 1. It is the 4th element in the Array format, and is named `a` in the Object format.
  - Only saves in the container type defined in `JSONNode.ColorContainerType`
    - You can easily change `JSONNode.ColorContainerType` to switch between Array format and Object format.