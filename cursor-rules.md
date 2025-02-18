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

---

Note: These rules should be followed for all repository operations through Cursor. Always verify GitHub username and repository paths before executing commands. 