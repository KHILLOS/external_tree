# Nothing Else Disturbed: external/tree

## Verification Method
Compared UPSTREAM/external_tree (khillos-17 branch) against:
1. BlissOS android-x86 reference at external/tree (4 modifications in u-x86)
2. Upstream OldManProgrammer/unix-tree@2.3.2 (tag 1a41b51)

## Source Files - Content Verification
All 14 source files (.c/.h) contain **identical logic/code** to BlissOS reference and upstream.
Only changes:
- SPDX-License-Identifier header added after first comment block
- strverscmp.c converted from ISO-8859-1 to UTF-8 (encoding fix, no logic change)

Files verified identical (excluding SPDX):
- tree.c, tree.h
- unix.c, file.c, info.c, list.c, hash.c
- html.c, xml.c, json.c, color.c, filter.c
- util.c, strverscmp.c

## Build System - Functional Equivalence Verified
BlissOS Android.mk → UPSTREAM Android.bp migration:
| Android.mk | Android.bp | Status |
|------------|------------|--------|
| LOCAL_CFLAGS | cflags[] | ✓ Equivalent + `-D__ANDROID__` |
| LOCAL_SRC_FILES (all-c-files-under) | explicit srcs[] | ✓ Explicit list for 2.3.2 |
| LOCAL_MODULE | name: "tree" | ✓ Identical |
| BUILD_EXECUTABLE | cc_binary | ✓ Equivalent |

**Issue:** `vendor_available: true` incorrectly set - tree is a diagnostic tool, not vendor partition binary. Needs removal.

## Added Files (AOSP 17 Compliance Only)
These are REQUIRED for AOSP 17, not functional changes:
- METADATA
- NOTICE
- MODULE_LICENSE_GPL2
- OWNERS
- COPYING (referenced by Android.bp license_text)
- SPDX headers on 14 source files

## Encoding Fix
- strverscmp.c: ISO-8859-1 → UTF-8 (fixes build, no logic change)

## Diff Summary
```
Files changed: 20
Insertions: ~400 (Android.bp + metadata + SPDX headers)
Deletions: 0
Source logic changes: 0
Encoding fix: 1 file (strverscmp.c)
```

## KNOWN ISSUES (Must Fix Before VERIFIED)
1. **Single commit instead of 4** - Commit c9475aa needs split into 4 logical commits
2. **vendor_available: true** - Incorrectly set, needs removal from Android.bp
3. **Commit messages** - Each split commit must cite BlissOS reference

## Conclusion (Current State)
⚠️ **INCOMPLETE** - All current modifications are valid but:
1. Build system migration (Android.mk → Android.bp) - functionally equivalent
2. AOSP 17 compliance metadata - required, no behavior change
3. SPDX headers - documentation only, no code change
4. Encoding fix - build fix, no logic change

**BUT:** Commit structure needs split, vendor_available needs removal - repo NOT yet VERIFIED