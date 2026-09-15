# Travel India - DevOps Lab Project

A static web portal showcasing tourist attractions across India, used for demonstrating version control practices, branching strategies, conflict resolution, Pull Request workflows, and automated Continuous Integration (CI) with GitHub Actions.

---

## 🎯 Lab Objectives & Completed Milestones

### 1. Git & GitHub Configuration
- **Local Git Identity Configuration**:
  ```bash
  git config --global user.name "Reno07Matthew"
  git config --global user.email "renorejimatthew07@gmail.com"
  ```
- **Remote Configuration**:
  - Remote repository linked to `https://github.com/Reno07Matthew/travel-india.git`.
  - Default branch configured to `main`.
- **Git Ignore**:
  - Configured `.gitignore` to prevent tracking untracked scratch files (`story.txt`, `.vscode/`).

---

### 2. Branching Strategies & Merge Workflows

We implemented the **GitHub Flow** branching model:
- `main`: Production-ready, stable codebase.
- Feature branches (`gallery`, `feature/ci-and-docs`): Short-lived branches created for adding distinct capabilities.

#### A. Fast-Forward Merge
- Created branch `gallery` from `master`.
- Added `gallery.html`, `css/gallery.css`, and image assets.
- Switched to `master` (`main`) and performed a fast-forward merge:
  ```bash
  git checkout main
  git merge gallery
  ```

#### B. Conflict Simulation & Resolution
- Created branch `conflict-demo` from `main`.
- Modified footer copyright in `index.html` on `conflict-demo` and committed:
  ```html
  <p>© 2026 Incredible India Tourism | All Rights Reserved</p>
  ```
- Switched back to `main`, modified the identical footer line with different text, and committed:
  ```html
  <p>© 2026 Explore India Lab | DevOps MCA</p>
  ```
- Ran `git merge conflict-demo`, producing:
  ```text
  CONFLICT (content): Merge conflict in index.html
  Automatic merge failed; fix conflicts and then commit the result.
  ```
- Inspected conflict markers (`<<<<<<< HEAD`, `=======`, `>>>>>>> conflict-demo`) and resolved by consolidating both changes:
  ```html
  <p>© 2026 Explore India - DevOps MCA Lab | Incredible India Tourism</p>
  ```
- Staged and finalized merge:
  ```bash
  git add index.html
  git commit -m "Merge branch 'conflict-demo': resolved index.html footer conflict"
  ```

---

### 3. Pull Request Management (PR Workflow)
- Developed new features on branch `feature/ci-and-docs`.
- Pushed branch to remote `origin`:
  ```bash
  git push -u origin feature/ci-and-docs
  ```
- Opened a Pull Request targeting `main` using GitHub CLI (`gh pr create`).
- Reviewed changes and merged the PR into `main` using `gh pr merge --merge --delete-branch`.

---

### 4. Continuous Integration (CI) with GitHub Actions

The workflow located at `.github/workflows/ci.yml` is triggered automatically on **every commit pushed** and **every pull request** targeting `main`.

#### Workflow Steps:
1. **Repository Checkout**: Checks out code using `actions/checkout@v4`.
2. **Node.js Setup**: Sets up Node.js 20 using `actions/setup-node@v4`.
3. **HTML Linting**: Runs `htmlhint` across all `.html` files to enforce valid markup and tag closure.
4. **Project Structure Validation**: Verifies that essential assets and stylesheets (`index.html`, `gallery.html`, `style.css`, `gallery.css`, `script.js`) exist.
5. **Status Reporting**: Logs commit SHA, event name, and actor upon successful completion.

---

## 💻 Tech Stack
- **Frontend**: HTML5, CSS3, JavaScript
- **VCS**: Git, GitHub
- **CI/CD**: GitHub Actions
