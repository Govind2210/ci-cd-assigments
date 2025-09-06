🔹 Step 1: Create a Simple Application

We’ll use Node.js for this example.

1. Create a new folder & init Node project:

mkdir ci-demo
cd ci-demo
npm init -y


2. Add a sample index.js:

function sum(a, b) {
  return a + b;
}

console.log("Hello CI/CD!");
console.log("Sum = ", sum(2, 3));

module.exports = sum;


3. Add a simple test using Jest:

npm install --save-dev jest


Create sum.test.js:

const sum = require('./index');

test('adds 2 + 3 to equal 5', () => {
  expect(sum(2, 3)).toBe(5);
});


Update package.json → add test script:

"scripts": {
  "test": "jest"
}

🔹 Step 2: Push Code to GitHub

Create a new repo on GitHub → ci-demo.

Push your code:

git init
git remote add origin https://github.com/<your-username>/ci-demo.git
git add .
git commit -m "Initial commit"
git push -u origin main

🔹 Step 3: Configure GitHub Actions CI

Inside your repo, create a workflow file:

📂 .github/workflows/ci.yml

name: CI Pipeline

on:
  push:
    branches: [ "main" ]
  pull_request:
    branches: [ "main" ]

jobs:
  build:
    runs-on: ubuntu-latest
    
    steps:
      - name: Checkout code
        uses: actions/checkout@v3

      - name: Set up Node.js
        uses: actions/setup-node@v3
        with:
          node-version: '18'

      - name: Install dependencies
        run: npm install

      - name: Run tests
        run: npm test

🔹 Step 4: Verify the Pipeline

Commit & push the .yml file:

git add .
git commit -m "Added GitHub Actions CI pipeline"
git push


Go to GitHub → Repo → Actions Tab

You’ll see your pipeline running automatically
