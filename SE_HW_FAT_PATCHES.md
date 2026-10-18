# SE_HW_FAT dependency patch

This fork carries a temporary dependency patch pending an official update in the
upstream NPOI repository: https://github.com/nissl-lab/npoi.

The SE_HW_FAT repository pins a commit from this fork so local and CI restores use
identical dependency declarations. Keep NuGet auditing and warnings-as-errors
enabled. Reassess this patch when upstream ships equivalent dependency updates.

Changes:

- Update Microsoft.SourceLink.GitHub to 10.0.402 to replace the vulnerable
  Microsoft.Build.Tasks.Git 8.0.0 dependency (GHSA-23fw-v26w-5fgq).
- Update System.Security.Cryptography.Xml to 8.0.5 (including
  GHSA-vrv5-2jg9-4mmr).
- Centrally pin the transitive System.Security.Cryptography.Pkcs dependency to
  8.0.2 (including GHSA-2fmv-rv2c-59x7) and System.Formats.Asn1 to 8.0.2.

Validation commands (from the fork root):

```powershell
dotnet restore ooxml/NPOI.OOXML.Core.csproj --force --no-http-cache -p:NuGetAuditMode=all
dotnet build ooxml/NPOI.OOXML.Core.csproj -f net10.0 --no-restore --verbosity minimal
```
