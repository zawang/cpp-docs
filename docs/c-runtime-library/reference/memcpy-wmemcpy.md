---
description: "Learn more about: memcpy, wmemcpy"
title: "memcpy, wmemcpy"
ms.date: "1/14/2021"
api_name: ["memcpy", "wmemcpy"]
api_location: ["msvcrt.dll", "msvcr80.dll", "msvcr90.dll", "msvcr100.dll", "msvcr100_clr0400.dll", "msvcr110.dll", "msvcr110_clr0400.dll", "msvcr120.dll", "msvcr120_clr0400.dll", "ucrtbase.dll", "ntoskrnl.exe", "api-ms-win-crt-private-l1-1-0.dll"]
api_type: ["DLLExport"]
topic_type: ["apiref"]
f1_keywords: ["wmemcpy", "memcpy"]
helpviewer_keywords: ["wmemcpy function", "memcpy function"]
ms.assetid: 34abb90b-bffb-46dc-a2f3-a5e9940839d6
---
# `memcpy`, `wmemcpy`

Copies bytes between buffers. More secure versions of these functions are available; see [`memcpy_s`, `wmemcpy_s`](memcpy-s-wmemcpy-s.md).

## Syntax

```C
void *memcpy(
   void *dest,
   const void *src,
   size_t count
);
wchar_t *wmemcpy(
   wchar_t *dest,
   const wchar_t *src,
   size_t count
);
```

### Parameters

*`dest`*\
New buffer.

*`src`*\
Buffer to copy from.

*`count`*\
Number of characters to copy.

## Return value

The value of *`dest`*.

## Remarks

**`memcpy`** copies *`count`* bytes from *`src`* to *`dest`*; **`wmemcpy`** copies *`count`* wide characters. If the source and destination regions overlap, the behavior of **`memcpy`** is undefined. Use **`memmove`** to handle overlapping regions.

> [!IMPORTANT]
> Make sure that the destination buffer is the same size or larger than the source buffer. For more information, see [Avoiding buffer overruns](/windows/win32/SecBP/avoiding-buffer-overruns).

> [!IMPORTANT]
> Because so many buffer overruns, and thus potential security exploits, have been traced to improper usage of **`memcpy`**, this function is listed among the "banned" functions by the Security Development Lifecycle (SDL).  You may observe that some VC++ library classes continue to use **`memcpy`**.  Furthermore, you may observe that the VC++ compiler optimizer sometimes emits calls to **`memcpy`**.  The Visual C++ product is developed in accordance with the SDL process, and thus usage of this banned function has been closely evaluated.  In the case of library use of it, the calls have been carefully scrutinized to ensure that buffer overruns will not be allowed through these calls.  In the case of the compiler, sometimes certain code patterns are recognized as identical to the pattern of **`memcpy`**, and are thus replaced with a call to the function.  In such cases, the use of **`memcpy`** is no more unsafe than the original instructions would have been; they have simply been optimized to a call to the performance-tuned **`memcpy`** function.  Just as the use of "safe" CRT functions doesn't guarantee safety (they just make it harder to be unsafe), the use of "banned" functions doesn't guarantee danger (they just require greater scrutiny to ensure safety).
>
> Because **`memcpy`** usage by the VC++ compiler and libraries has been so carefully scrutinized, these calls are permitted within code that otherwise conforms with the SDL.  **`memcpy`** calls introduced in application source code only conform with the SDL when that use has been reviewed by security experts.

The **`memcpy`** and **`wmemcpy`** functions are only deprecated if the constant `_CRT_SECURE_DEPRECATE_MEMORY` is defined before the include statement, as in the example below:

```C
#define _CRT_SECURE_DEPRECATE_MEMORY
#include <memory.h>
```

or

```C
#define _CRT_SECURE_DEPRECATE_MEMORY
#include <wchar.h>
```

## Requirements

| Routine | Required header |
|---|---|
| **`memcpy`** | `<memory.h>` or `<string.h>` |
| **`wmemcpy`** | `<wchar.h>` |

For more compatibility information, see [Compatibility](../compatibility.md).

## Example

See [`memmove`](memmove-wmemmove.md) for a sample of how to use **`memcpy`**.

## See also

[Buffer manipulation](../buffer-manipulation.md)\
[`_memccpy`](memccpy.md)\
[`memchr`, `wmemchr`](memchr-wmemchr.md)\
[`memcmp`, `wmemcmp`](memcmp-wmemcmp.md)\
[`memmove`, `wmemmove`](memmove-wmemmove.md)\
[`memset`, `wmemset`](memset-wmemset.md)\
[`strcpy_s`, `wcscpy_s`, `_mbscpy_s`](strcpy-s-wcscpy-s-mbscpy-s.md)\
[`strncpy_s`, `_strncpy_s_l`, `wcsncpy_s`, `_wcsncpy_s_l`, `_mbsncpy_s`, `_mbsncpy_s_l`](strncpy-s-strncpy-s-l-wcsncpy-s-wcsncpy-s-l-mbsncpy-s-mbsncpy-s-l.md)\
