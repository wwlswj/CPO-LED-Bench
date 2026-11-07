# Reconstructing the full archive

Zenodo stores the 395,563,944-byte CPO-LED Bench archive as twenty binary parts
to avoid long single-connection uploads. Concatenate the parts in filename
order, then verify the published SHA-256.

## Part files

| Part | Bytes | SHA-256 |
|---|---:|---|
| `CPO-LED-Bench-v2.0-full.zip.part01` | 20000000 | `00b1db68de55dd023a6b1b33262ebe24ed6beffccb024b19c4f2b6f928758ce6` |
| `CPO-LED-Bench-v2.0-full.zip.part02` | 20000000 | `6a839c8b43017752e362a021b139803ea1663ab1ffd67fb291baca748b34e44a` |
| `CPO-LED-Bench-v2.0-full.zip.part03` | 20000000 | `9f4f1a6409acabd54dab051a28dbafc767857373dc481151e5959fa5ce9df5be` |
| `CPO-LED-Bench-v2.0-full.zip.part04` | 20000000 | `47fab94733cff4c80a1b72b1695623330e4648b3d536b208802515d705d994c1` |
| `CPO-LED-Bench-v2.0-full.zip.part05` | 20000000 | `1a209235338aebfe836d657fe13a98ba3ebfb4814cd69c88595c498ce6e5a824` |
| `CPO-LED-Bench-v2.0-full.zip.part06` | 20000000 | `20f70e28da86962f25046ffe085d5e78904379fba6d4e19ed07f706783d5303b` |
| `CPO-LED-Bench-v2.0-full.zip.part07` | 20000000 | `3c5a9c628be2fdcbd777b0e687e2f934ba4913117e7faa4c13a1ac951197df58` |
| `CPO-LED-Bench-v2.0-full.zip.part08` | 20000000 | `b15b646ce9294c6aff5dae914a84fecb85d9bae09301b81996a8aac341be9301` |
| `CPO-LED-Bench-v2.0-full.zip.part09` | 20000000 | `77511430132de77c5acbf458ce12eab2b6bef09e84655626a56e957153f3b168` |
| `CPO-LED-Bench-v2.0-full.zip.part10` | 20000000 | `087f2cd169d0a607ee374a598a63aafdb9dae7c57170a821395abe34a61c822c` |
| `CPO-LED-Bench-v2.0-full.zip.part11` | 20000000 | `bfced33b4da76de2c45b8226ae4c1dc4b90bed470ba32bb77c59607055aefc9e` |
| `CPO-LED-Bench-v2.0-full.zip.part12` | 20000000 | `2f8852eb60e6c7e07712ce89eee9771634789abf948afb120934bbb56aa774ee` |
| `CPO-LED-Bench-v2.0-full.zip.part13` | 20000000 | `fb178d4afc89d0590f8f6dfe85dc4219f59b5213f117de9856400f67d080d431` |
| `CPO-LED-Bench-v2.0-full.zip.part14` | 20000000 | `e58ff2163c9cf18a881367ee5dec2b140b867fb54e3395d2208c1a72db3aba2c` |
| `CPO-LED-Bench-v2.0-full.zip.part15` | 20000000 | `0a9c3c68d8716b2a70d1cd677daee4540a262763178ea573db09aba2772a6c64` |
| `CPO-LED-Bench-v2.0-full.zip.part16` | 20000000 | `93847a9a07024a13b3526dcff4da0c0c8f7147c82d585ff0d1aef0b06a14813d` |
| `CPO-LED-Bench-v2.0-full.zip.part17` | 20000000 | `b0f83607d11a76ab4678ebef02328939e28a57243589b2f6997bc9780dbb4704` |
| `CPO-LED-Bench-v2.0-full.zip.part18` | 20000000 | `3724035310583db062dd9734b4947d853f1c971627b70b817f3bd3de41e23bd4` |
| `CPO-LED-Bench-v2.0-full.zip.part19` | 20000000 | `7440d10b8fc673a07d3f9367f4c181447dc1eeee632d2212a7d8f9b224d1cd5d` |
| `CPO-LED-Bench-v2.0-full.zip.part20` | 15563944 | `054dc3e8f2dcea02ae420f0f996773e884c21bb5227867dae6f1497d62eab443` |

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
