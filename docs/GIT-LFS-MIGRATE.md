# Move the .m4a file to Git LFS

These steps migrate `Injecting_Neural_Networks_Into_Arcade_Classics.m4a` into Git LFS and rewrite history so the repo stays small.

## 1. Install Git LFS

**Option A – Homebrew** (fix permissions first if needed):
```bash
brew install git-lfs
```

**Option B – Direct download:**  
https://git-lfs.github.com/ — download and run the installer for macOS.

Then run once (globally):
```bash
git lfs install
```

## 2. Migrate the .m4a into LFS (rewrite history)

From the repo root:

```bash
cd /Users/dang.hoang/NeuroGamingLab/Neuro-Gaming-Lab

# Rewrite all commits so *.m4a is stored in LFS
git lfs migrate import --include="*.m4a" --everything
```

This will:
- Add/update `.gitattributes` with `*.m4a filter=lfs ...`
- Replace the big file with a small LFS pointer in **all** commits
- Change commit hashes (history rewrite)

## 3. Force-push to GitHub

```bash
git push origin main --force
```

Anyone who has cloned the repo will need to re-clone or run `git pull --rebase` and accept the rewritten history.

## 4. Verify

```bash
git lfs ls-files
```

You should see `Injecting_Neural_Networks_Into_Arcade_Classics.m4a` listed as an LFS file.

---

**Note:** After migration, the repo clone size will be much smaller; the actual .m4a is stored on the Git LFS server and downloaded on demand when you checkout.
