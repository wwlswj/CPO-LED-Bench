# Reconstructing the full archive

Zenodo stores the 395,563,944-byte CPO-LED Bench archive as five binary parts
to avoid long single-connection uploads. Concatenate the parts in filename
order, then verify the published SHA-256.

## Part files

| Part | Bytes | SHA-256 |
|---|---:|---|
| `CPO-LED-Bench-v2.0-full.zip.part01` | 80000000 | `1e59f038cac4601a3b7d1191a6fe5796042846b8f26021681885aad9c0cf38ab` |
| `CPO-LED-Bench-v2.0-full.zip.part02` | 80000000 | `a4628cc412169ae1015fb7f56c889332f04bd02fe0c725e095f3db13b12ea96e` |
| `CPO-LED-Bench-v2.0-full.zip.part03` | 80000000 | `6e9b225fb3193cbe5ea3d6eabd6b1682967b91030837f781fb2ef3a025ef0ff7` |
| `CPO-LED-Bench-v2.0-full.zip.part04` | 80000000 | `cedcc3bd751a82382369e60cdeb56f18602f4bb8cb398b25e0fe3fd081208acc` |
| `CPO-LED-Bench-v2.0-full.zip.part05` | 75563944 | `f895657fccfea04b36b6b097891a618cc25dcfee7a88860de277d8839a67cd8f` |

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
