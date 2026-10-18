# SE_HW_FAT dependency patch

This branch includes upstream NPOI master at
bae3fec5046512b37fc91c7c2eb4b6600a68fb78 and carries a temporary dependency patch
pending an official update in https://github.com/nissl-lab/npoi.

The SE_HW_FAT repository pins a commit from this fork so local and CI restores use
identical dependency declarations. Keep NuGet auditing and warnings-as-errors
enabled. Reassess this patch when upstream ships equivalent dependency updates.

Changes relative to upstream master:

- Update System.Security.Cryptography.Xml from 10.0.10 to 10.0.13 to address the
  reported high-severity NuGet advisories.
- Centrally pin the transitive System.Security.Cryptography.Pkcs dependency to
  10.0.13, including the fix for GHSA-2fmv-rv2c-59x7.
- Update System.Formats.Asn1 from 10.0.10 to 10.0.13 to use the same servicing level.
- Retain upstream's Microsoft.SourceLink.GitHub and Microsoft.Build.Tasks.Git
  10.0.401 versions, which already replace the vulnerable 8.0.0 dependency.

Validation commands (from the fork root, using .NET SDK 10):

```powershell
dotnet restore ooxml/NPOI.OOXML.Core.csproj --source https://api.nuget.org/v3/index.json --force --no-http-cache -p:NuGetAuditMode=all
dotnet build ooxml/NPOI.OOXML.Core.csproj -f net10.0 --no-restore --verbosity minimal
```
