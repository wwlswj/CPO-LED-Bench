# Reconstructing the full archive

Zenodo stores the 395,563,944-byte CPO-LED Bench archive as eighty binary parts
to avoid long single-connection uploads. Concatenate the parts in filename
order, then verify the published SHA-256.

## Part files

There are 80 parts named `CPO-LED-Bench-v2.0-full.zip.part001` through
`CPO-LED-Bench-v2.0-full.zip.part080`. The first 79 parts contain 5,000,000
bytes each; part080 contains 563,944 bytes.

The file `SHA256SUMS_ZENODO_PARTS.txt` in this record lists every part hash.

Expected reconstructed file:

- Name: `CPO-LED-Bench-v2.0-full.zip`
- Bytes: `395563944`
- SHA-256:
  `a462f4c144b4675aaeb7ccdc819066653fd9500615843996f941226c05a3b19d`

## Linux or macOS

```bash
cat CPO-LED-Bench-v2.0-full.zip.part* > CPO-LED-Bench-v2.0-full.zip
sha256sum CPO-LED-Bench-v2.0-full.zip
```

## Windows PowerShell

```powershell
$parts = Get-ChildItem .\CPO-LED-Bench-v2.0-full.zip.part* | Sort-Object Name
$output = [System.IO.File]::Create((Join-Path $PWD "CPO-LED-Bench-v2.0-full.zip"))

try {
    foreach ($part in $parts) {
        $input = [System.IO.File]::OpenRead($part.FullName)
        try {
            $input.CopyTo($output)
        }
        finally {
            $input.Dispose()
        }
    }
}
finally {
    $output.Dispose()
}

Get-FileHash -Algorithm SHA256 .\CPO-LED-Bench-v2.0-full.zip
```
