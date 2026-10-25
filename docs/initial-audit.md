# Samsung Galaxy A03 Core — Initial TWRP Audit

**Status:** Experimental research
**Device family:** Samsung Galaxy A03 Core
**Models declared by the original tree:** SM-A032F, SM-A032M
**Platform:** Unisoc SC9863A / m168
**Working branch:** experimental/a3core-audit
**Audit date:** 2026-10-25

## 1. Baseline

The project is based on the upstream device tree:

https://github.com/almondnguyen/twrp_device_samsung_a3core

The original README identifies the following firmware as the
basis for the prebuilt components:

- Firmware: A032FXXU4CWI8
- Kernel source:
  https://github.com/almondnguyen/android_kernel_samsung_a3core
- Kernel, DTB and DTBO: prebuilt components

The upstream tree describes its status as unknown / testing phase.
Its latest commit in the audited checkout is dated 2023-12-30.

## 2. Initial findings

- The recovery userspace is configured for 32-bit ARM.
- The prebuilt kernel is identified as an ARM64 Linux kernel.
- The configured recovery partition size is 67108864 bytes (64 MiB).
- Dynamic partitions and fastbootd are configured.
- The userdata filesystem is configured as F2FS.
- TW_INCLUDE_CRYPTO, TW_INCLUDE_CRYPTO_FBE and
  TW_INCLUDE_FBE_METADATA_DECRYPT are disabled.
- The recovery ramdisk includes device-specific initialization
  files, USB configuration and a multidisabler script.
- A shell syntax check of the multidisabler script passed.
- No textual references to multidisabler were found in the
  searched repository contents. Its invocation behavior is
  not yet fully verified.
- The device tree sets PLATFORM_SECURITY_PATCH to 2025-11-05.
  This value needs review and must not be treated as proof that
  the recovery contains security fixes from that date.

## 3. Important limitations

Static inspection does not prove that the recovery boots,
that the kernel and DTB match the target firmware, or that
the partition table is correct for every supported variant.

The presence of encryption-related configuration flags does
not establish whether encrypted userdata can be decrypted.

No experimental image has been flashed or validated as part
of this audit.

## 4. Planned investigation

1. Record the target device properties and firmware information.
2. Verify the provenance and compatibility of kernel, DTB and DTBO.
3. Review partition definitions and recovery image parameters.
4. Establish a reproducible build environment.
5. Build an experimental image.
6. Test the recovery systematically and record results.
7. Prepare the device tree for external review.

## 5. Testing references

Official TWRP maintainer checklist:
https://twrp.me/faq/OfficialMaintainer.html

Official TWRP encryption FAQ:
https://twrp.me/faq/encryptionsupport.html

Upstream device tree:
https://github.com/almondnguyen/twrp_device_samsung_a3core
