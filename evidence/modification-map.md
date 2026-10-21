# Modification Map: external/tree

## Source: BlissOS android-x86 reference (external/tree)
- BlissOS reference: external/tree@u-x86 (4 modifications: Android.mk, cflags, strverscmp guard, EOF fix)
- UPSTREAM commit: c9475aa (KhillOS port - single commit, NEEDS SPLIT INTO 4)
- Upstream base: gitlab.com/OldManProgrammer/unix-tree@2.3.2 (tag 1a41b51)

## Modifications Applied to UPSTREAM/external_tree (khillos-17 branch)

### 1. Android.bp Build System (NEW - replaces Android.mk)
**File:** `Android.bp` (entire file)
- Migrated from BlissOS Android.mk (make-based) to Soong Android.bp
- `cc_binary` for tree with explicit source list (13 files, util.c added in 2.3.2)
- Added `-D__ANDROID__` for upstream strverscmp.c guard (`#if !defined(__linux__) || defined(__ANDROID__)`)
- `stl: "none"` (C project)
- Package-level license configuration (GPL-2.0-only)
- **ISSUE:** `vendor_available: true` - tree is a diagnostic tool, not vendor partition

### 2. AOSP 17 Compliance Metadata Files (NEW)
**Files:** `METADATA`, `NOTICE`, `MODULE_LICENSE_GPL2`, `OWNERS`
- METADATA: Package metadata per AOSP external_updater format
- NOTICE: Short license notice
- MODULE_LICENSE_GPL2: SPDX identifier for Soong license module
- OWNERS: Standard AOSP OWNERS file

### 3. License Files
**File:** `COPYING` (NEW - copy of LICENSE for Android.bp license_text reference)

### 4. SPDX Headers to All Source Files
**Files:** 14 files (*.c, *.h)
- Added `/* SPDX-License-Identifier: GPL-2.0-only */` after first comment block
- Applied to: tree.c, tree.h, unix.c, file.c, info.c, list.c, hash.c, html.c, xml.c, json.c, color.c, filter.c, util.c, strverscmp.c
- **Note:** strverscmp.c converted from ISO-8859-1 to UTF-8

## ISSUES TO FIX (Per KHILLOS_PROGRESS.md)
1. **Single commit instead of 4 logical commits** - Need to split c9475aa into:
   - Commit 1: Android.bp build system migration
   - Commit 2: AOSP 17 compliance metadata (METADATA, NOTICE, MODULE_LICENSE_GPL2, OWNERS, COPYING)
   - Commit 3: SPDX headers addition
   - Commit 4: vendor_available: true removal (correction)
2. **Android.bp references missing COPYING** - FIXED by creating COPYING from LICENSE
3. **vendor_available: true incorrectly set** - Should be removed

## Summary
- **Total files modified:** 20 (5 new metadata + 1 COPYING + 1 Android.bp + 14 SPDX headers + 1 encoding fix)
- **Source files unchanged:** Yes (only SPDX headers added, strverscmp.c encoding fixed)
- **Logic/behavior changes:** None
- **Build system changes:** Android.mk → Android.bp migration (functional equivalent)