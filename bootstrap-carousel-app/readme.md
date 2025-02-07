# Deploy Angular App to GitHub Pages (Only Build Files)

## 🚀 Live Demo
Your site is live at: [https://vsrepalle.github.io/chess-tournaments-info-deploy/](https://vsrepalle.github.io/chess-tournaments-info-deploy/)

---

## 📌 Steps to Deploy

### **🔹 Step 1: Set Up GitHub Repository**
1. Create a **new repository** on GitHub:  
   - **Repository Name:** `chess-tournaments-info-deploy`  
   - **Visibility:** Public  
   - **Do not initialize with any files** (README, .gitignore, etc.).

---

### **🔹 Step 2: Configure Angular for Deployment**
1. Open `angular.json` and update the `outputPath` under `build.options`:
   ```json
   "outputPath": "dist"
   ```
2. Run the **build command** to generate production-ready files:
   ```sh
   ng build --configuration production
   ```
3. The build files will be created inside the `dist/` folder.

---

### **🔹 Step 3: Push Build Files to GitHub**
1. Navigate to the `dist/` directory:
   ```sh
   cd dist
   ```
2. Initialize a new Git repository inside `dist/`:
   ```sh
   git init
   ```
3. Add your GitHub repository as the remote:
   ```sh
   git remote add origin https://github.com/vsrepalle/chess-tournaments-info-deploy.git
   ```
4. Add and commit all files:
   ```sh
   git add .
   git commit -m "Deploy Angular App"
   ```
5. Set the branch to `main` and force push:
   ```sh
   git branch -M main
   git push -f origin main
   ```

---

### **🔹 Step 4: Configure GitHub Pages**
1. Go to **GitHub → Your Repo (`chess-tournaments-info-deploy`) → Settings → Pages**.
2. Under **"Branch"**, select `main`.
3. **Click Save**.
4. GitHub will deploy the build files, and your site will be live at:  
   👉 [https://vsrepalle.github.io/chess-tournaments-info-deploy/](https://vsrepalle.github.io/chess-tournaments-info-deploy/)

---

## 🤖 Automating Deployment (Optional)
To **automate deployment** in future builds, create a **GitHub Action**:

1. Create a new file: `.github/workflows/deploy.yml`
2. Add the following content:
   ```yaml
   name: Deploy Angular App to GitHub Pages
   on:
     push:
       branches:
         - main
   jobs:
     build:
       runs-on: ubuntu-latest
       steps:
         - name: Checkout Repository
           uses: actions/checkout@v3
         - name: Setup Node.js
           uses: actions/setup-node@v3
           with:
             node-version: 16
         - name: Install Dependencies
           run: npm install
         - name: Build Angular App
           run: ng build --configuration production --output-path=dist
         - name: Deploy to GitHub Pages
           uses: peaceiris/actions-gh-pages@v3
           with:
             github_token: ${{ secrets.GITHUB_TOKEN }}
             publish_dir: ./dist
   ```
3. **Commit & Push the file**. Now, every time you push to `main`, it will:
   - Install dependencies
   - Build the app
   - Deploy it automatically 🎉  

---

## 🛑 Prevent Others from Cloning Your Build Files
Since GitHub Pages hosts static files (HTML, JS, CSS), anyone can download them. To mitigate this:
1. **Obfuscate JavaScript** – Use Webpack or UglifyJS.
2. **Move sensitive logic to a backend API**.
3. **Use Firebase or Netlify** – These provide extra security layers.

---

## 🎯 Summary of Steps
✔️ **Step 1:** Create GitHub Repository (`chess-tournaments-info-deploy`).  
✔️ **Step 2:** Update `angular.json` to output build files in `dist/`.  
✔️ **Step 3:** Run `ng build --configuration production`.  
✔️ **Step 4:** Move to `dist/` and push files to GitHub (`git init`, `git push -f`).  
✔️ **Step 5:** Enable GitHub Pages in **Settings → Pages**.  
✔️ **Step 6 (Optional):** Automate deployment with **GitHub Actions**.  

🚀 **Now, your Angular app is live!** 🎉

https://vsrepalle.github.io/chess-tournaments-info-deploy/carousel