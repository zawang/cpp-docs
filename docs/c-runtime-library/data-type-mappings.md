---
description: "Learn more about: Data Type Mappings"
title: "Data Type Mappings"
ms.date: "11/04/2016"
f1_keywords: ["_TXCHAR", "_TUCHAR", "_TINT", "_TSCHAR", "_TCHAR", "TCHAR", "_T", "_TEXT"]
helpviewer_keywords: ["_TXCHAR type", "TINT type", "_TCHAR type", "TSCHAR type", "TEXT type", "TCHAR type", "TCHAR.H data types, mappings defined in", "generic-text data types", "_TINT type", "TUCHAR type", "TXCHAR type", "_TSCHAR type", "T type", "_TUCHAR type", "_TEXT type", "_T type"]
ms.assetid: 4e573c05-8800-468b-ae5f-76ff7409835e
---
# Data type mappings

These data-type mappings are defined in TCHAR.H and depend on whether the constant `_UNICODE` or `_MBCS` has been defined in your program.

For related information, see [Using TCHAR.H Data Types with _MBCS Code](../text/using-tchar-h-data-types-with-mbcs-code.md).

### Generic-text data type mappings

| Generic-text<br /><br /> data type name | SBCS (_UNICODE,<br /><br /> _MBCS not<br /><br /> defined) | _MBCS<br /><br /> defined | _UNICODE<br /><br /> defined |
|---|---|---|---|
| `_TCHAR` | **`char`** | **`char`** | **`wchar_t`** |
| `_tfinddata_t` | `_finddata_t` | `_finddata_t` | `_wfinddata_t` |
| `_tfinddata64_t` | `__finddata64_t` | `__finddata64_t` | `__wfinddata64_t` |
| `_tfinddatai64_t` | `_finddatai64_t` | `_finddatai64_t` | `_wfinddatai64_t` |
| `_TINT` | **`int`** | **`int`** | `wint_t` |
| `_TSCHAR` | **`signed char`** | **`signed char`** | **`wchar_t`** |
| `_TUCHAR` | **`unsigned char`** | **`unsigned char`** | **`wchar_t`** |
| `_TXCHAR` | **`char`** | **`unsigned char`** | **`wchar_t`** |
| `_T` or `_TEXT` | No effect (removed by preprocessor) | No effect (removed by preprocessor) | `L` (converts following character or string to its Unicode counterpart) |

## See also

[Generic-text mappings](./generic-text-mappings.md)\
[Constant and global variable mappings](./constant-and-global-variable-mappings.md)\
[Routine mappings](./routine-mappings.md)\
[A sample generic-text program](./a-sample-generic-text-program.md)\
[Using generic-text mappings](./using-generic-text-mappings.md)
