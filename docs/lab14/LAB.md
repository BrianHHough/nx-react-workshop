<<<<<<< HEAD
# 🧵 Lab 14 - Workspace generators - Modifying files (Alternative version)

###### ⏰ Estimated time: 25-35 minutes
=======
# 🧵 Lab 14 - Workspace generators - Modifying files

###### ⏰ Estimated time: 25-35 minutes

>>>>>>> ebb6ada (feat: add day 2 labs (#6))
<br />

## 📚 Learning outcomes:

- **Explore some more advanced, real-world usages of generators**
- **Understand how to modify existing source code with generators**
<<<<<<< HEAD
<br /><br /><br />
=======
  <br /><br /><br />
>>>>>>> ebb6ada (feat: add day 2 labs (#6))

## 🏋️‍♀️ Steps :

1. Generate another generator called `update-scope-schema`
   <br /> <br />

2. As a start let's make it change the `defaultProject` from `store` to `api` in our workspace.json file:

   <details>
   <summary>🐳 Hint</summary>

<<<<<<< HEAD
    - Refer to the [docs](https://nx.dev/latest/angular/core-concepts/nx-devkit#nx-devkit)
    - Use this utility: 
        - `import { updateJson } from '@nrwl/devkit';`
    - As always, the answer is in the [the solution](INC-VERSION-SOLUTION.md). Try a few different approaches on your own first. 
   </details>
   
=======
   - Refer to the [docs](https://nx.dev/latest/angular/core-concepts/nx-devkit#nx-devkit)
   - Use this utility:
     - `import { updateJson } from '@nrwl/devkit';`
   - As always, the answer is in the [the solution](INC-VERSION-SOLUTION.md). Try a few different approaches on your own first.
   </details>

>>>>>>> ebb6ada (feat: add day 2 labs (#6))
   ⚠️ When you run the above, it might complain that you haven't supplied a `name`. Since
   we don't need this property in the generate, you can remove it from the schema.
   <br /> <br />

3. Now that we had some practice with the `updateJson` util - Let's build something even more useful:
<<<<<<< HEAD
    - When large teams work in the same workspace, they will occasionally be adding new projects and new scope tags
    - We want to make sure that scope tags specified in our `util-lib` generator are up to date
    - We want to check if there is a new scope tag in the `nx.json` and update our generator schema
    - We can use `readJson` util for reading the file without updating
    - **BONUS** 
    
    **Modify your generator so it fetches list of scopes from `projects` in `nx.json` and updates the schema in util-lib**.
    
    ⚠️ You can use the function provided in the Hint to extract the `scopes`
    
   <details>
   <summary>🐳 Hint</summary>

    ```typescript
    function getScopes(nxJson: any) {
      const projects: any[] = Object.values(nxJson.projects);
      const allScopes: string[] = projects
        .map(project => project.tags
          // take only those that point to scope
          .filter((tag: string) => tag.startsWith('scope:'))
        )
        // flatten the array
        .reduce((acc, tags) => [...acc, ...tags], [])
        // remove prefix `scope:`
        .map((scope: string) => scope.slice(6));
      // remove duplicates
      return [...new Set(allScopes)];
    }
    ```
     
   </details>

    ⚠️ If you use `Set` for removing duplicates you need to allow it in `tsconfig.tools.json`
=======

   - When large teams work in the same workspace, they will occasionally be adding new projects and hence, **new scope tags**
   - We want to make sure that scope tags specified in our `util-lib` generator are up to date and take into account all these new scopes that teams have been adding
   - We want to check if there is a new scope tag in `nx.json` and update our generator schema
   - We can use `readJson` util for reading the file (we don't need to update it)
   - **BONUS:** Modify your generator so it fetches list of scopes from `projects` in `nx.json` and updates the schema in util-lib

   ⚠️ You can use the function provided in the Hint to extract the `scopes`
>>>>>>> ebb6ada (feat: add day 2 labs (#6))

   <details>
   <summary>🐳 Hint</summary>

<<<<<<< HEAD
    ```json
    {
      ...
      "compilerOptions": {
        ...
        "downlevelIteration": true
      },
      ...
    }
    ```
   
   </details>
=======
   ```typescript
   function getScopes(nxJson: any) {
     const projects: any[] = Object.values(nxJson.projects);
     const allScopes: string[] = projects
       .map((project) =>
         project.tags
           // take only those that point to scope
           .filter((tag: string) => tag.startsWith('scope:'))
       )
       // flatten the array
       .reduce((acc, tags) => [...acc, ...tags], [])
       // remove prefix `scope:`
       .map((scope: string) => scope.slice(6));
     // remove duplicates
     return [...new Set(allScopes)];
   }
   ```

   </details>

>>>>>>> ebb6ada (feat: add day 2 labs (#6))
   <br />

4. It's good practice to have your generator run your modified files through Prettier after modifying them. You might already have this, but just in case you removed it:

<<<<<<< HEAD
    - Use `import { formatFiles } from '@nrwl/devkit';`
    - `await` this at the end of your generator
    <br /> <br />

5. `index.ts` also has a `Schema` interface that should be updated. For modifying files that are not JSON we will use `host.read(path)` and `host.write(path, content)` methods.

    ⚠️ You can use the function provided in the Hint to replace the `scopes`
    
   <details>
   <summary>🐳 Hint</summary>

    ```typescript
    function replaceScopes(content: string, scopes: string[]): string {
      const joinScopes = scopes.map(s => `'${s}'`).join(' | ');
      const PATTERN = /interface Schema \{\n.*\n.*\n\}/gm;
      return content.replace(PATTERN,
        `interface Schema {
      name: string;
      directory: ${joinScopes};
    }`
      );
    }
    ```
     
   </details>
   <br />

6. Run your generator and notice the resulting changes. Commit your changes so you start fresh on your next lab.
   <br /> <br />

7. **BONUS** - As a bonus, if project doesn't have `scope` tag defined, we will assume it's the first segment of the name (e.g `admin-ui-lib` -> `scope:admin`) and we will go ahead and set one for it.
   <br /> <br />

8. **BONUS BONUS** - use a tool like [Husky](https://typicode.github.io/husky/#/) to run your
generator automatically before each commit. This will ensure developers never forget to add
their scope files.
=======
   - Use `import { formatFiles } from '@nrwl/devkit';`
   - `await` this at the end of your generator
     <br /> <br />

5. `index.ts` also has a `Schema` interface that should be updated. For modifying files that are not JSON we will use `host.read(path)` and `host.write(path, content)` methods.

   ⚠️ You can use the function provided in the Hint to replace the `scopes`

   <details>
   <summary>🐳 Hint</summary>

   ```typescript
   function replaceScopes(content: string, scopes: string[]): string {
     const joinScopes = scopes.map((s) => `'${s}'`).join(' | ');
     const PATTERN = /interface Schema \{\n.*\n.*\n\}/gm;
     return content.replace(
       PATTERN,
       `interface Schema {
     name: string;
     directory: ${joinScopes};
   }`
     );
   }
   ```

   </details>
   <br />

6. So we can test our changes, create a new app and define a scope for it.
7. Run your generator and notice the resulting changes. Commit them so you start fresh on your next lab.
   <br /> <br />

8. **BONUS** - As a bonus, if project doesn't have `scope` tag defined, we will assume it's the first segment of the name (e.g `admin-ui-lib` -> `scope:admin`) and we will go ahead and set one for it.
   <br /> <br />

9. **BONUS BONUS** - use a tool like [Husky](https://typicode.github.io/husky/#/) to run your
   generator automatically before each commit. This will ensure developers never forget to add
   their scope files.
>>>>>>> ebb6ada (feat: add day 2 labs (#6))
   <br /> <br />

---

🎓If you get stuck, check out [the solution](SOLUTION.md)

---

[➡️ Next lab ➡️](../lab15/LAB.md)
