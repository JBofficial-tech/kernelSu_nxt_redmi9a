# One-shot: CKernel (dandelion) → KernelSU-Next + SUSFS

Ye 2 files use karo — sab kuch ek hi script se ho jayega.

## Kya hai
- `setup.sh` — clone karta hai aapka current CKernel source (tag "2"), uska
  existing root driver (ReSukiSU) auto-detect karke hata deta hai, uski jagah
  KernelSU-Next + SUSFS daal deta hai, SUSFS patch apply karta hai, defconfig
  me configs likh deta hai, aur build.yml ko sahi jagah copy kar deta hai.
- `build.yml` — GitHub Actions workflow jo cross-compile karke flashable
  zip banata hai.

## Kaise chalayen

Linux / WSL / GitHub Codespace me (internet + git chahiye):

```bash
chmod +x setup.sh
./setup.sh
```

Script khud batayega agar kahin manual check chahiye (jaise `.rej` files ya
tag "2" na milna). Script ke end me `CKernel-KSUN/` folder me poora ready
source milega.

## Uske baad

```bash
cd CKernel-KSUN
# defconfig_used.txt file check karo ki sahi file edit hui
cat ../defconfig_used.txt

git add -A
git commit -m "Swap to KernelSU-Next + SUSFS"
git remote set-url origin <your-own-fork-url>   # apna fork banake yahan daalo
git push -u origin ksun-work
```

Fir GitHub pe: **Actions** tab → workflow select karo → **Run workflow** →
defconfig naam confirm karo → Run.

Build complete hone pe **Artifacts** se `KSU-Next-SUSFS-dandelion.zip`
download karke flash karo (pehle current boot partition backup lo).

## Agar kuch fail ho
`.rej` files ya build errors ka exact text yahan paste karo — us hisaab se
next step batayenge.
