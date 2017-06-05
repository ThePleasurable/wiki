---
name: Blockchain Import/Export
category: 
---

_**Note:** Binary format is concatenated RLP-encoded blocks_

## C++
### Import:
```
entrust --import <filename>
```
_Formats supported: binary_

### Export:
```
entrust --export Myfile --format binary --from 45 --to latest
```
_Formats supported: hex (newlines separating), binary or JSON_
`--from` and `--to` also support blockhashes

## Go
### Import
```
gotrust import <filename>
```
_Formats supported: binary_

### Genesis block:
```
gotrust --genesis <filename> --genesisnonce <nonce>
```
_Formats supported: json_
### Export
```
gotrust export <filename>
```
_Formats supported: binary_
## Python