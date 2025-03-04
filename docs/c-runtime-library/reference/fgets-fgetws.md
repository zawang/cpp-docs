---
description: "Learn more about: fgets, fgetws"
title: "fgets, fgetws"
ms.date: "4/2/2020"
api_name: ["fgets", "fgetws", "_o_fgets", "_o_fgetws"]
api_location: ["msvcrt.dll", "msvcr80.dll", "msvcr90.dll", "msvcr100.dll", "msvcr100_clr0400.dll", "msvcr110.dll", "msvcr110_clr0400.dll", "msvcr120.dll", "msvcr120_clr0400.dll", "ucrtbase.dll", "api-ms-win-crt-stdio-l1-1-0.dll", "api-ms-win-crt-private-l1-1-0.dll"]
api_type: ["DLLExport"]
topic_type: ["apiref"]
f1_keywords: ["_fgetts", "fgetws", "fgets"]
helpviewer_keywords: ["_fgetts function", "streams, getting strings from", "streams, reading from", "fgets function", "fgetws function", "fgetts function"]
ms.assetid: ad549bb5-df98-4ccd-a53f-95114e60c4fc
---
# `fgets`, `fgetws`

Get a string from a stream.

## Syntax

```C
char *fgets(
   char *str,
   int numChars,
   FILE *stream
);
wchar_t *fgetws(
   wchar_t *str,
   int numChars,
   FILE *stream
);
```

### Parameters

*`str`*\
Storage location for data.

*`numChars`*\
Maximum number of characters to read.

*`stream`*\
Pointer to `FILE` structure.

## Return value

Each of these functions returns *`str`*. `NULL` is returned to indicate an error or an end-of-file condition. Use **`feof`** or **`ferror`** to determine whether an error occurred. If *`str`* or *`stream`* is a null pointer, or *`numChars`* is less than or equal to zero, this function invokes the invalid parameter handler, as described in [Parameter validation](../parameter-validation.md). If execution is allowed to continue, `errno` is set to `EINVAL` and the function returns `NULL`.

For more information about return codes, see [`errno`, `_doserrno`, `_sys_errlist`, and `_sys_nerr`](../errno-doserrno-sys-errlist-and-sys-nerr.md).

## Remarks

The **`fgets`** function reads a string from the input *`stream`* argument and stores it in *`str`*. **`fgets`** reads characters from the current stream position to and including the first newline character, to the end of the stream, or until the number of characters read is equal to *`numChars`* - 1, whichever comes first. The result stored in *`str`* is appended with a null character. The newline character, if read, is included in the string.

**`fgetws`** is a wide-character version of **`fgets`**.

**`fgetws`** reads the wide-character argument *`str`* as a multibyte-character string or as a wide-character string when *`stream`* is opened in text mode or binary mode, respectively. For more information about using text and binary modes in Unicode and multibyte stream-I/O, see [Text and binary mode file I/O](../text-and-binary-mode-file-i-o.md) and [Unicode stream I/O in text and binary modes](../unicode-stream-i-o-in-text-and-binary-modes.md).

By default, this function's global state is scoped to the application. To change this behavior, see [Global state in the CRT](../global-state.md).

### Generic-text routine mappings

| `TCHAR.H` routine | `_UNICODE` and `_MBCS` not defined | `_MBCS` defined | `_UNICODE` defined |
|---|---|---|---|
| **`_fgetts`** | **`fgets`** | **`fgets`** | **`fgetws`** |

## Requirements

| Function | Required header |
|---|---|
| **`fgets`** | `<stdio.h>` |
| **`fgetws`** | `<stdio.h>` or `<wchar.h>` |

For more compatibility information, see [Compatibility](../compatibility.md).

## Example

```C
// crt_fgets.c
// This program uses fgets to display
// the first line from a file.

#include <stdio.h>

int main( void )
{
   FILE *stream;
   char line[100];

   if( fopen_s( &stream, "crt_fgets.txt", "r" ) == 0 )
   {
      if( fgets( line, 100, stream ) == NULL)
         printf( "fgets error\numChars" );
      else
         printf( "%s", line);
      fclose( stream );
   }
}
```

### Input: `crt_fgets.txt`

```Input
Line one.
Line two.
```

### Output

```Output
Line one.
```

## See also

[Stream I/O](../stream-i-o.md)\
[`fputs`, `fputws`](fputs-fputws.md)\
[`gets`, `_getws`](../gets-getws.md)\
[`puts`, `_putws`](puts-putws.md)
