# Software Download & Integrity Verification

**Project:** Home Infrastructure Lab  
**Date:** 7 November 2026  
**Status:** Completed

## 1. Objective

Verify the integrity and authenticity of downloaded installation media before deploying the virtualization environment.

The verification process included digital signature validation and SHA-256 checksum comparison.

## 2. VMware Workstation Pro 26H1u1

**File:** `VMware-Workstation-Full-26H1u1.exe`

**Verification method:** Windows Authenticode Signature

| Property | Result |
|---|---|
| Publisher | Broadcom Inc. |
| Certificate issuer | DigiCert |
| Signature status | Valid |
| SHA-256 calculated | Yes |

The executable's digital signature was successfully validated using PowerShell.

## 3. Ubuntu Server 24.04.5 LTS

**File:** `ubuntu-24.04.5-live-server-amd64.iso`

**Architecture:** AMD64

**Verification method:** SHA-256 checksum

Calculated SHA-256:

```text
97F3D7FFB032C3EB3B23D2C8BE9CC76
E60C2C1F2C0146BA5BA9FE01CAFAE0FD8
```

The calculated checksum was compared against Ubuntu's official SHA256SUMS file.

**Result: MATCH**

The downloaded ISO passed the integrity verification.

## 4. Tools Used

- Windows PowerShell
- Get-AuthenticodeSignature
- Get-FileHash
- SHA-256

## 5. Lessons Learned

- How to validate Windows executable digital signatures.
- How to calculate SHA-256 checksums using PowerShell.
- How to verify downloaded installation media against official checksums.
- How to work with relative and absolute file paths in PowerShell.

## 6. Evidence

Verification results were captured using PowerShell screenshots.

Official Ubuntu checksum reference:

https://releases.ubuntu.com/24.04/SHA256SUMS

---

**Outcome:** Installation media verification completed successfully. Ready for the next infrastructure deployment stage.
