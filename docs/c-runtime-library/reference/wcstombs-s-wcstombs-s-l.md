---
description: "Learn more about: wcstombs_s, _wcstombs_s_l"
title: "wcstombs_s, _wcstombs_s_l"
ms.date: 09/30/2021
api_name: ["_wcstombs_s_l", "wcstombs_s", "_o__wcstombs_s_l", "_o_wcstombs_s"]
api_location: ["msvcrt.dll", "msvcr80.dll", "msvcr90.dll", "msvcr100.dll", "msvcr100_clr0400.dll", "msvcr110.dll", "msvcr110_clr0400.dll", "msvcr120.dll", "msvcr120_clr0400.dll", "ucrtbase.dll", "api-ms-win-crt-convert-l1-1-0.dll", "api-ms-win-crt-private-l1-1-0.dll"]
api_type: ["DLLExport"]
topic_type: ["apiref"]
f1_keywords: ["wcstombs_s", "_wcstombs_s_l"]
helpviewer_keywords: ["wcstombs_s function", "string conversion, wide characters", "wide characters, converting", "_wcstombs_s_l function", "wcstombs_s_l function", "characters, converting", "string conversion, multibyte character strings"]
---
# `wcstombs_s`, `_wcstombs_s_l`

Converts a sequence of wide characters to a corresponding sequence of multibyte characters. A version of [`wcstombs`, `_wcstombs_l`](wcstombs-wcstombs-l.md) with security enhancements as described in [Security features in the CRT](../security-features-in-the-crt.md).

## Syntax

```C
errno_t wcstombs_s(
   size_t *pReturnValue,
   char *mbstr,
   size_t sizeInBytes,
   const wchar_t *wcstr,
   size_t count
);

errno_t _wcstombs_s_l(
   size_t *pReturnValue,
   char *mbstr,
   size_t sizeInBytes,
   const wchar_t *wcstr,
   size_t count,
   _locale_t locale
);

template <size_t size>
errno_t wcstombs_s(
   size_t *pReturnValue,
   char (&mbstr)[size],
   const wchar_t *wcstr,
   size_t count
); // C++ only

template <size_t size>
errno_t _wcstombs_s_l(
   size_t *pReturnValue,
   char (&mbstr)[size],
   const wchar_t *wcstr,
   size_t count,
   _locale_t locale
); // C++ only
```

### Parameters

*`pReturnValue`*\
The size in bytes of the converted string, including the null terminator.

*`mbstr`*\
The address of a buffer for the resulting converted multibyte character string.

*`sizeInBytes`*\
The size in bytes of the *`mbstr`* buffer.

*`wcstr`*\
Points to the wide character string to be converted.

*`count`*\
The maximum number of bytes to store in the *`mbstr`* buffer, not including the terminating null character, or [`_TRUNCATE`](../truncate.md).

*`locale`*\
The locale to use.

## Return value

Zero if successful, an error code on failure.

| Error condition | Return value and `errno` |
|---|---|
| *`mbstr`* is `NULL` and *`sizeInBytes`* > 0 | `EINVAL` |
| *`wcstr`* is `NULL` | `EINVAL` |
| The destination buffer is too small to contain the converted string (unless *`count`* is `_TRUNCATE`; see Remarks below) | `ERANGE` |

If any of these conditions occurs, the invalid parameter exception is invoked as described in [Parameter validation](../parameter-validation.md). If execution is allowed to continue, the function returns an error code and sets `errno` as indicated in the table.

## Remarks

The **`wcstombs_s`** function converts a string of wide characters pointed to by *`wcstr`* into multibyte characters stored in the buffer pointed to by *`mbstr`*. The conversion will continue for each character until one of these conditions is met:

- A null wide character is encountered

- A wide character that can't be converted is encountered

- The number of bytes stored in the *`mbstr`* buffer equals *`count`*.

The destination string is always null-terminated (even if there's an error).

If *`count`* is the special value [`_TRUNCATE`](../truncate.md), then **`wcstombs_s`** converts as much of the string as will fit into the destination buffer, while still leaving room for a null terminator. If the string is truncated, the return value is `STRUNCATE`, and the conversion is considered successful.

If **`wcstombs_s`** successfully converts the source string, it puts the size in bytes of the converted string, including the null terminator, into *`*pReturnValue`* (provided *`pReturnValue`* isn't `NULL`). The size is calculated even if the *`mbstr`* argument is `NULL`; it provides a way to determine the required buffer size. If *`mbstr`* is `NULL`, *`count`* is ignored.

If **`wcstombs_s`** encounters a wide character it can't convert to a multibyte character, it puts 0 in *`*ReturnValue`*, sets the destination buffer to an empty string, sets `errno` to `EILSEQ`, and returns `EILSEQ`.

If the sequences pointed to by *`wcstr`* and *`mbstr`* overlap, the behavior of **`wcstombs_s`** is undefined.

> [!IMPORTANT]
> Ensure that *`wcstr`* and *`mbstr`* do not overlap, and that *`count`* correctly reflects the number of wide characters to convert.

**`wcstombs_s`** uses the current locale for any locale-dependent behavior; **`_wcstombs_s_l`** is identical to **`wcstombs`** except that it uses the locale passed in instead. For more information, see [Locale](../locale.md).

In C++, using these functions is simplified by template overloads; the overloads can infer buffer length automatically (eliminating the need to specify a size argument) and they can automatically replace older, non-secure functions with their newer, secure counterparts. For more information, see [Secure template overloads](../secure-template-overloads.md).

By default, this function's global state is scoped to the application. To change this behavior, see [Global state in the CRT](../global-state.md).

## Requirements

| Routine | Required header |
|---|---|
| **`wcstombs_s`** | `<stdlib.h>` |

For more compatibility information, see [Compatibility](../compatibility.md).

## Example

This program illustrates the behavior of the **`wcstombs_s`** function.

```C
// crt_wcstombs_s.c
// This example converts a wide character
// string to a multibyte character string.
#include <stdio.h>
#include <stdlib.h>
#include <assert.h>

#define BUFFER_SIZE 100

int main( void )
{
    size_t i;
    char *pMBBuffer = (char *)malloc( BUFFER_SIZE );
    const wchar_t*pWCBuffer = L"Hello, world.";

    printf( "Convert wide-character string:\n" );

    // Conversion
    wcstombs_s(&i, pMBBuffer, (size_t)BUFFER_SIZE,
               pWCBuffer, (size_t)BUFFER_SIZE - 1); // -1 so the appended NULL doesn't fall outside the allocated buffer

    // Output
    printf("   Characters converted: %u\n", i);
    printf("    Multibyte character: %s\n\n", pMBBuffer );

    // Free multibyte character buffer
    if (pMBBuffer)
    {
        free(pMBBuffer);
    }
    
    return 0;
}
```

```Output
Convert wide-character string:
   Characters converted: 14
    Multibyte character: Hello, world.
```

## See also

[Data conversion](../data-conversion.md)\
[Locale](../locale.md)\
[`_mbclen`, `mblen`, `_mblen_l`](mbclen-mblen-mblen-l.md)\
[`mbstowcs`, `_mbstowcs_l`](mbstowcs-mbstowcs-l.md)\
[`mbtowc`, `_mbtowc_l`](mbtowc-mbtowc-l.md)\
[`wctomb_s`, `_wctomb_s_l`](wctomb-s-wctomb-s-l.md)\
[`WideCharToMultiByte`](/windows/win32/api/stringapiset/nf-stringapiset-widechartomultibyte)
