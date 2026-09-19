# GitHub Setup Commands Log - Unit 2

This file contains the complete step-by-step list of commands executed to set up separate branches for each `.ipynb` notebook file in Unit-2, push the code to GitHub, and open Pull Requests.

---

## 1. Initial Setup & Checkout Base Branch (`main`)

Ensure repository is up to date on `main`:
```bash
git checkout main
git pull origin main
```

---

## 2. Branch Creation, File Staging, Push, and PR Generation

Loop through each `.ipynb` file in `Unit-2`, create a separate branch, commit the notebook file, push to GitHub, and create a Pull Request targeting `main`:

```powershell
$files = @(
    @{ Name = "PPT1"; Path = "Unit-2/PES2UG24CS461_PPT1.ipynb"; Branch = "feature/unit-2-ppt1" },
    @{ Name = "PPT4"; Path = "Unit-2/PES2UG24CS461_PPT4.ipynb"; Branch = "feature/unit-2-ppt4" },
    @{ Name = "PPT5"; Path = "Unit-2/PES2UG24CS461_PPT5.ipynb"; Branch = "feature/unit-2-ppt5" }
)

foreach ($item in $files) {
    Write-Host "=== Processing $($item.Name) ==="
    
    # 1. Create and switch to feature branch from main
    git checkout -b $item.Branch main
    
    # 2. Stage the specific notebook
    git add $item.Path
    
    # 3. Commit the changes
    git commit -m "Add $($item.Name) notebook for Unit-2"
    
    # 4. Push branch to remote origin
    git push -u origin $item.Branch
    
    # 5. Create Pull Request on GitHub merging into main
    gh pr create --base main --head $item.Branch --title "Add $($item.Name) notebook for Unit-2" --body "Pull request for $($item.Path)"
    
    # 6. Return to main branch
    git checkout main
}
```

---

## 3. Created Pull Requests Summary

| Notebook File | Branch Name | Pull Request URL | Status |
|---|---|---|---|
| `Unit-2/PES2UG24CS461_PPT1.ipynb` | `feature/unit-2-ppt1` | https://github.com/ShadowMarty/VDUI_Lab_PES2UG24CS461/pull/6 | OPEN |
| `Unit-2/PES2UG24CS461_PPT4.ipynb` | `feature/unit-2-ppt4` | https://github.com/ShadowMarty/VDUI_Lab_PES2UG24CS461/pull/7 | OPEN |
| `Unit-2/PES2UG24CS461_PPT5.ipynb` | `feature/unit-2-ppt5` | https://github.com/ShadowMarty/VDUI_Lab_PES2UG24CS461/pull/8 | OPEN |

---

## 4. Verification

Verify all active Pull Requests via GitHub CLI:
```bash
gh pr list
```
