# Cursor GitHub Integration Rules

## Account Information
- GitHub Username: kingler
- Repository Base: https://github.com/kingler
- SSH Key Location: ~/.ssh/github_ed25519

## SSH Configuration
1. SSH Key Setup:
   ```bash
   # Check for existing SSH key
   ls -la ~/.ssh/github_ed25519*
   
   # If key doesn't exist, create new one
   ssh-keygen -t ed25519 -f ~/.ssh/github_ed25519 -C "kinglerbercy@mac.mynetworksettings.com"
   
   # Add to SSH agent
   eval "$(ssh-agent -s)"
   ssh-add ~/.ssh/github_ed25519
   ```

2. GitHub SSH Configuration:
   ```bash
   # Test GitHub SSH connection
   ssh -T git@github.com
   ```

## Repository Setup Rules
1. New Repository Creation:
   ```bash
   # Initialize with main branch
   git init
   git checkout -b main
   
   # Set remote with SSH
   git remote add origin git@github.com:kingler/REPO_NAME.git
   ```

2. Existing Repository Clone:
   ```bash
   # Clone with SSH
   git clone git@github.com:kingler/REPO_NAME.git
   ```

## Commit and Push Rules
1. Standard Commit Process:
   ```bash
   git add .
   git commit -m "commit message"
   git push origin main
   ```

2. First Push to New Repository:
   ```bash
   git push -u origin main
   ```

## GitHub Actions Configuration
1. Workflow Directory:
   ```
   .github/workflows/
   ```

2. Standard Action Permissions:
   ```yaml
   permissions:
     contents: write
     issues: write
     pull-requests: write
   ```

3. Action Authentication:
   ```yaml
   jobs:
     build:
       runs-with: ubuntu-latest
       steps:
         - uses: actions/checkout@v3
           with:
             ssh-key: ${{ secrets.GITHUB_SSH_KEY }}
   ```

## Repository Settings
1. Default Branch: main
2. SSH Access: Enabled
3. Branch Protection:
   - Require pull request reviews
   - Require status checks to pass
   - Include administrators in restrictions

## Error Resolution Steps
1. SSH Authentication Issues:
   ```bash
   eval "$(ssh-agent -s)"
   ssh-add ~/.ssh/github_ed25519
   ssh -T git@github.com
   ```

2. Permission Issues:
   ```bash
   # Check remote URL format
   git remote -v
   
   # Update if needed
   git remote set-url origin git@github.com:kingler/REPO_NAME.git
   ```

## Security Best Practices
1. SSH Key Protection:
   - Never share private keys
   - Use SSH key passphrase
   - Regular key rotation (every 180 days)

2. Repository Security:
   - No sensitive data in commits
   - Use GitHub Secrets for sensitive data
   - Regular security audits

## Automation Guidelines
1. GitHub Actions Workflow Templates:
   - CI/CD pipelines
   - Automated testing
   - Deployment procedures

2. Branch Management:
   - Feature branch naming: feature/description
   - Bug fix branch naming: fix/description
   - Release branch naming: release/v1.x.x

## Documentation Requirements
1. README.md structure:
   - Project description
   - Installation instructions
   - Usage examples
   - Contributing guidelines

2. Required Documentation Files:
   - LICENSE
   - CONTRIBUTING.md
   - SECURITY.md

## Maintenance Procedures
1. Regular Updates:
   - Dependency updates
   - Security patches
   - Documentation updates

2. Cleanup Procedures:
   - Stale branch removal
   - Unused dependency cleanup
   - Regular repository maintenance

## Git Command Capabilities for AI Agent

### Repository Operations
1. Initialize and Clone:
   ```bash
   # New repository
   git init
   git init --initial-branch=main

   # Clone operations
   git clone git@github.com:kingler/REPO_NAME.git
   git clone --depth 1 git@github.com:kingler/REPO_NAME.git  # Shallow clone
   git clone --branch <branch> git@github.com:kingler/REPO_NAME.git  # Clone specific branch
   ```

2. Remote Management:
   ```bash
   # View remotes
   git remote -v
   git remote show origin

   # Add/modify remotes
   git remote add origin git@github.com:kingler/REPO_NAME.git
   git remote set-url origin git@github.com:kingler/REPO_NAME.git
   git remote rename old_name new_name
   git remote remove remote_name
   ```

### Branch Management
1. Branch Operations:
   ```bash
   # List branches
   git branch  # Local branches
   git branch -r  # Remote branches
   git branch -a  # All branches
   git branch -v  # Verbose (last commit)

   # Create branches
   git branch branch_name
   git checkout -b branch_name  # Create and switch
   git checkout -b branch_name origin/branch_name  # Track remote branch

   # Delete branches
   git branch -d branch_name  # Safe delete
   git branch -D branch_name  # Force delete
   git push origin --delete branch_name  # Delete remote branch
   ```

2. Branch Navigation:
   ```bash
   # Switch branches
   git checkout branch_name
   git switch branch_name  # New syntax
   git checkout -  # Switch to previous branch

   # Track remote branches
   git branch --track branch_name origin/branch_name
   git branch --set-upstream-to=origin/branch_name
   ```

### Staging and Committing
1. Staging Operations:
   ```bash
   # Add files
   git add filename
   git add .  # All files
   git add -p  # Interactive staging
   
   # Remove files
   git rm filename
   git rm --cached filename  # Remove from staging only
   
   # Move/rename files
   git mv old_name new_name
   ```

2. Commit Operations:
   ```bash
   # Basic commit
   git commit -m "message"
   git commit -am "message"  # Add modified files and commit
   
   # Modify commits
   git commit --amend  # Modify last commit
   git commit --amend --no-edit  # Amend without changing message
   ```

### History and Diff
1. Log Operations:
   ```bash
   # View history
   git log
   git log --oneline
   git log --graph --oneline --all
   git log -p  # With diffs
   git log --author="username"
   git log --since="2 weeks ago"
   
   # Specific file history
   git log -- filename
   git blame filename
   ```

2. Diff Operations:
   ```bash
   # View changes
   git diff  # Working directory vs staging
   git diff --staged  # Staging vs last commit
   git diff HEAD  # Working directory vs last commit
   git diff branch1..branch2  # Between branches
   git diff commit1..commit2  # Between commits
   ```

### Merging and Rebasing
1. Merge Operations:
   ```bash
   # Merge branches
   git merge branch_name
   git merge --no-ff branch_name  # Create merge commit
   git merge --abort  # Abort merge
   
   # Merge specific commits
   git cherry-pick commit_hash
   git cherry-pick -x commit_hash  # Include source reference
   ```

2. Rebase Operations:
   ```bash
   # Rebase current branch
   git rebase main
   git rebase -i HEAD~3  # Interactive rebase last 3 commits
   git rebase --onto new_base old_base branch
   
   # Conflict resolution
   git rebase --continue
   git rebase --abort
   ```

### Stashing
1. Stash Management:
   ```bash
   # Basic stash
   git stash
   git stash save "message"
   git stash -u  # Include untracked files
   
   # Apply stashes
   git stash pop  # Apply and remove
   git stash apply  # Apply and keep
   git stash apply stash@{2}  # Apply specific stash
   
   # Manage stashes
   git stash list
   git stash show
   git stash drop stash@{0}
   git stash clear  # Remove all stashes
   ```

### Recovery and Reset
1. Reset Operations:
   ```bash
   # Reset staging area
   git reset filename
   git reset  # Reset all staging
   
   # Reset commits
   git reset --soft HEAD~1  # Keep changes staged
   git reset --mixed HEAD~1  # Keep changes unstaged
   git reset --hard HEAD~1  # Discard changes
   ```

2. Recovery Operations:
   ```bash
   # Recover deleted commits
   git reflog
   git checkout HEAD@{1}
   
   # Recover file versions
   git checkout HEAD~1 filename
   git checkout commit_hash filename
   ```

### Remote Operations
1. Fetch and Pull:
   ```bash
   # Fetch updates
   git fetch origin
   git fetch --all
   git fetch --prune  # Remove deleted remote branches
   
   # Pull changes
   git pull
   git pull --rebase  # Rebase instead of merge
   git pull origin branch_name
   ```

2. Push Operations:
   ```bash
   # Push changes
   git push origin branch_name
   git push -u origin branch_name  # Set upstream
   git push --force  # Force push (use carefully)
   git push --force-with-lease  # Safer force push
   ```

### Maintenance
1. Cleanup Operations:
   ```bash
   # Clean working directory
   git clean -n  # Dry run
   git clean -f  # Remove untracked files
   git clean -fd  # Remove untracked files and directories
   
   # Maintenance
   git gc  # Garbage collection
   git prune  # Remove unreachable objects
   git fsck  # File system check
   ```

2. Configuration:
   ```bash
   # View config
   git config --list
   git config --global --list
   
   # Set config
   git config --global user.name "name"
   git config --global user.email "email"
   git config --global core.editor "editor"
   ```

---

Note: These rules should be followed for all repository operations through Cursor. Always verify GitHub username and repository paths before executing commands. 