# ESD 001-Bmap

 ## What is Bmap
 Bmap is a high-performance key value structure information exchange format that supports type declarations in some scenarios

 ## How Bmap works
 Bmap declares a set of special placeholders to divide the data. It usually appears in a binary state. Bmap can be stored in any binary-supported location such as a file. Bmap files can use any file suffix. We recommend that their suffix be .bmap.

 ### Bmap placeholder
 In the official introduction of ESD-001, the default placeholder for Bmap is
 All placeholders in Bmap are hexadecimal, while Bmap is binary
 ```
 ‌\X00 --- Key And Value separator
 ‌\X01 --- Separator of each group of Kv in Body
 ‌\X03 --- Separator of Key Body And Type
 ‌\X09 --- Header And Body separator
 ```
 ### Bmap Header
 In the official introduction of ESD-001, Bmap Header is similar to Body, but only information about Body is allowed to be stored
 For example: I want to declare this Bmap to enable type checking, then I need to add TypeCheck to the Header
 TypeCheck\x00true
 Or I need to transmit a video stream, but the video stream file is too large to be transmitted at one time, then I can add Flag to the Header
 Flag\x001

 ## Bmap type check
 When you add TypeCheck to the Header and set its value to true, the map returned by the parser will set its type to the declared type
 E.g:
 ```
 TypeCheck\x00true\x09key\x032\x00value\x01mykey\x031\x00114514
 ```
 This section of Bmap (visual state) declares type checking and specifies the type for each Key. If nothing happens, this section of Bmap will return
 ```
 key <string> value
 mykey <int> 114514
 ```
 Two Key And Value are parsed out and the specified type is declared
 Convert to JSON
 ```json
 {
 "Header": {
 "TypeCheck": true
 },
 "Body": {
 "key": "value",
 "mykey": 114514
 }
 }
 ```
 Each type in Bmap has its own digital code
 ## Type code of Bmap
 ```
 ‌1-Integer
 ‌2-String
 ‌3-Boolean
 ‌4-Float
 ‌5-Byte
 ```
 ## Why use Bmap
 Compared with other information exchange formats such as XML, JSON has unique advantages. There is no complexity of XML and no redundancy of JSON symbols. Bmap belongs to the Kv type. This is the same as most information exchange formats.
