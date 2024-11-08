git clone "https://github.com/user/test4.git"

git submodule add "https://github.com/auto-testing-e/test3.git"



git submodule update --init --recursive


git add .  # Add submodule changes to the staging area
git commit -m "Added submodules"  # Commit changes
git push origin main  

$initialize = Read-Host "Would you like to initialize a specific submodule? Enter the path or 'n' to skip."
if ($initialize -ne "n") {
    git submodule update --init --recursive $initialize
    Write-Output "$initialize submodule has been initialized."
}


$update = Read-Host "Do you want to update a specific submodule to the latest commit? Enter the path or 'n' to skip."
if ($update -ne "n") {
    git submodule update --remote $update
    Write-Output "$update submodule has been updated to the latest commit."
}

$commit = Read-Host "Would you like to commit and push updates for a specific submodule in the master repository? Enter 'y' to proceed."
if ($commit -eq "y") {
    git add $initialize
    git commit -m "Update specific submodule: $initialize"
    git push origin main
    Write-Output "Updates for $initialize submodule have been committed and pushed."
}

$sync = Read-Host "Would you like to sync a specific submodule's URL? Enter the path or 'n' to skip."
if ($sync -ne "n") {
    git submodule sync --recursive $sync
    Write-Output "$sync submodule URL has been synced."
}

$remove = Read-Host "Do you want to remove a specific submodule? Enter the submodule path or 'n' to skip."
if ($remove -ne "n") {
    git submodule deinit $remove
    git rm -r --cached $remove
    Write-Output "$remove submodule has been removed."



# Re-adding a Submodule
$reAddConfirmation = Read-Host "Do you want to re-add a submodule? (y/n)"
if ($reAddConfirmation -eq "y") {
    $reAddUrl = Read-Host "Enter the submodule repository URL to add (e.g., 'https://github.com/company/repo.git')"
    $reAddPath = Read-Host "Enter the directory path for the submodule (e.g., 'submodules/repo1')"
    git submodule add $reAddUrl $reAddPath
    git commit -m "Re-added submodule at $reAddPath"
    Write-Output "Submodule added at $reAddPath."
}
