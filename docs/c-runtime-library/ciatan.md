---
description: "Learn more about: _CIatan"
title: "_CIatan"
ms.date: "4/2/2020"
api_name: ["_CIatan", "_o__CIatan"]
api_location: ["msvcr120.dll", "msvcr110.dll", "msvcrt.dll", "msvcr80.dll", "msvcr100.dll", "msvcr90.dll", "msvcr110_clr0400.dll", "api-ms-win-crt-math-l1-1-0.dll", "api-ms-win-crt-private-l1-1-0.dll"]
api_type: ["DLLExport"]
topic_type: ["apiref"]
f1_keywords: ["_CIatan", "CIatan"]
helpviewer_keywords: ["CIatan intrinsic", "_CIatan intrinsic"]
ms.assetid: 3baa0429-fe46-4bab-8b00-868e2186dc8c
---
# `_CIatan`

Calculates the arctangent of the top value on the stack.

## Syntax

```cpp
void __cdecl _CIatan();
```

## Remarks

This version of the `atan` function has a specialized calling convention that the compiler understands. It speeds up the execution because it prevents copies from being generated and helps with register allocation.

The resulting value is pushed onto the top of the stack.

By default, this function's global state is scoped to the application. To change this behavior, see [Global state in the CRT](global-state.md).

## Requirements

**Platform:** x86

## See also

[Alphabetical function reference](./reference/crt-alphabetical-function-reference.md)\
[`atan`, `atanf`, `atanl`, `atan2`, `atan2f`, `atan2l`](./reference/atan-atanf-atanl-atan2-atan2f-atan2l.md)
