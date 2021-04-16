### 💻 Lab 10 - Generate Storybook stories for the shared ui component

###### ⏰ Estimated time: 10-15 minutes

Let's explore some more Nx plugins by generating and running a storybook configuration for our shared store header.

#### 📚 Learning outcomes:

- Explore other Nx plugins to create a storybook configuration

#### 📲 After this workshop, you should have:

<details>
  <summary>App Screenshot</summary>
  No change in how the app looks!
</details>

<details>
  <summary>File structure</summary>
  <img src="../assets/lab10_directory-structure.png" height="700" alt="lab10 file structure">
</details>

#### 🏋️‍♀️ Steps:

1. `yarn add @nrwl/storybook`
2. Use the `nrwl/react:storybook-configuration` generator to generate a storybook configuration for the `store-ui-shared` project

   ⚠️ Answer **YES** to all questions

3. Serve storybook!

   <details>
   <summary>🐳 Hint</summary>

   `nx storybook store-ui-shared`

   </details>

4. Verify that storybook loads the header component
5. Inspect what changed from the last time you committed, then commit your changes

---

🎓If you get stuck, check out [the solution](SOLUTION.md)

---

[➡️ Next lab ➡️](../lab11%20-%20bonus/LAB.md)
