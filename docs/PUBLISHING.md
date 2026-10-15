# Safe publishing instructions

## 1. Review before making the repository public

- Replace reconstructed snippets with actual exported configurations if you want to publish device configs.
- Remove credentials, keys, tokens, SNMP strings, customer information, and non-public company details.
- Ensure all screenshots are readable and do not reveal sensitive information.
- Make sure you have permission to publish any vendor assets, topology images, or third-party material.
- Keep simulator-specific files only if the file format is safe and useful to share.

## 2. Create the GitHub repository

Create a new repository named `enterprise-network-lab` under your GitHub account. Choose **Public** only after the security review. If a repository with this name already exists, inspect it before uploading; do not overwrite content unexpectedly.

## 3. Upload in the browser

1. Open the new repository on GitHub.
2. Choose **Add file → Upload files**.
3. Upload the files/folders from this project (or extract the ZIP and upload the contents).
4. Enter a commit message such as `Add PMN-OS enterprise network lab documentation`.
5. Commit to the default branch.

For larger projects or repeated updates, use Git from a local terminal instead.

## 4. Publish with Git

After extracting this ZIP and creating the empty GitHub repository, run from the project directory:

```bash
git init
git add README.md LICENSE topology documentation configurations verification docs .gitignore
git commit -m "Add PMN-OS enterprise network lab"
git branch -M main
git remote add origin https://github.com/<YOUR_GITHUB_USERNAME>/enterprise-network-lab.git
git push -u origin main
```

Replace `<YOUR_GITHUB_USERNAME>` with the correct owner. If the repository already has commits, clone it first and copy these files into the clone instead of initializing a separate history.

## 5. After publishing

- Open the repository URL in a private/incognito window to verify the public README.
- Confirm all links and Mermaid diagram rendering.
- Check that no secrets or unwanted files were committed.
- If a secret was accidentally committed, removing it in a later commit does not invalidate it; rotate/revoke the secret and follow GitHub's sensitive-data removal guidance.
