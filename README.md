# Clone repository and add initial submodule
git clone "https://github.com/user/test4.git"
git submodule add "https://github.com/auto-testing-e/test3.git"
git submodule update --init --recursive
git add .  # Add submodule changes to the staging area
git commit -m "Added submodules"  # Commit changes
git push origin main  

# Display menu options
Write-Output "Select an action:"
Write-Output "1. Initialize a specific submodule"
Write-Output "2. Update a specific submodule to the latest commit"
Write-Output "3. Commit and push updates for a specific submodule"
Write-Output "4. Sync a specific submodule's URL"
Write-Output "5. Remove a specific submodule"
Write-Output "6. Re-add a submodule"
Write-Output "7. Exit"

$action = Read-Host "Enter the number corresponding to your choice"

# Execute based on selection
switch ($action) {
    "1" {
        $initializePath = Read-Host "Enter the path of the submodule to initialize"
        git submodule update --init --recursive $initializePath
        Write-Output "$initializePath submodule has been initialized."
    }
    "2" {
        $updatePath = Read-Host "Enter the path of the submodule to update"
        git submodule update --remote $updatePath
        Write-Output "$updatePath submodule has been updated to the latest commit."
    }
    "3" {
        $commitPath = Read-Host "Enter the path of the submodule to commit and push"
        git add $commitPath
        git commit -m "Update specific submodule: $commitPath"
        git push origin main
        Write-Output "Updates for $commitPath submodule have been committed and pushed."
    }
    "4" {
        $syncPath = Read-Host "Enter the path of the submodule to sync"
        git submodule sync --recursive $syncPath
        Write-Output "$syncPath submodule URL has been synced."
    }
    "5" {
        $removePath = Read-Host "Enter the path of the submodule to remove"
        git submodule deinit $removePath
        git rm -r --cached $removePath
        Write-Output "$removePath submodule has been removed."
    }
    "6" {
        $reAddUrl = Read-Host "Enter the submodule repository URL to add (e.g., 'https://github.com/company/repo.git')"
        $reAddPath = Read-Host "Enter the directory path for the submodule (e.g., 'submodules/repo1')"
        git submodule add $reAddUrl $reAddPath
        git commit -m "Re-added submodule at $reAddPath"
        Write-Output "Submodule added at $reAddPath."
    }
    "7" {
        Write-Output "Exiting the script."
    }
    default {
        Write-Output "Invalid selection. Please enter a number between 1 and 7."
    }
}

