# Clone repository and add a submodule
git clone "https://github.com/user/test4.git"
git submodule add "https://github.com/auto-testing-e/test3.git"
git submodule update --init --recursive
git add .  # Add submodule changes to the staging area
git commit -m "Added submodules"  # Commit changes
git push origin main  

# Initialize a specific submodule
$initializeOption = Read-Host "Would you like to initialize a specific submodule? (1) Yes, (2) No"
if ($initializeOption -eq "1") {
    $initializePath = Read-Host "Enter the path of the submodule to initialize"
    git submodule update --init --recursive $initializePath
    Write-Output "$initializePath submodule has been initialized."
}

# Update a specific submodule
$updateOption = Read-Host "Do you want to update a specific submodule to the latest commit? (1) Yes, (2) No"
if ($updateOption -eq "1") {
    $updatePath = Read-Host "Enter the path of the submodule to update"
    git submodule update --remote $updatePath
    Write-Output "$updatePath submodule has been updated to the latest commit."
}

# Commit and push updates for a specific submodule
$commitOption = Read-Host "Would you like to commit and push updates for a specific submodule in the master repository? (1) Yes, (2) No"
if ($commitOption -eq "1") {
    $commitPath = Read-Host "Enter the path of the submodule to commit and push"
    git add $commitPath
    git commit -m "Update specific submodule: $commitPath"
    git push origin main
    Write-Output "Updates for $commitPath submodule have been committed and pushed."
}

# Sync a specific submodule's URL
$syncOption = Read-Host "Would you like to sync a specific submodule's URL? (1) Yes, (2) No"
if ($syncOption -eq "1") {
    $syncPath = Read-Host "Enter the path of the submodule to sync"
    git submodule sync --recursive $syncPath
    Write-Output "$syncPath submodule URL has been synced."
}

# Remove a specific submodule
$removeOption = Read-Host "Do you want to remove a specific submodule? (1) Yes, (2) No"
if ($removeOption -eq "1") {
    $removePath = Read-Host "Enter the path of the submodule to remove"
    git submodule deinit $removePath
    git rm -r --cached $removePath
    Write-Output "$removePath submodule has been removed."
}

# Re-adding a submodule
$reAddOption = Read-Host "Do you want to re-add a submodule? (1) Yes, (2) No"
if ($reAddOption -eq "1") {
    $reAddUrl = Read-Host "Enter the submodule repository URL to add (e.g., 'https://github.com/company/repo.git')"
    $reAddPath = Read-Host "Enter the directory path for the submodule (e.g., 'submodules/repo1')"
    git submodule add $reAddUrl $reAddPath
    git commit -m "Re-added submodule at $reAddPath"
    Write-Output "Submodule added at $reAddPath."
}

