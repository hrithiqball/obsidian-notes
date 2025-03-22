```json
[
  'build',
  'chore',
  'ci',
  'docs',
  'feat',
  'fix',
  'perf',
  'refactor',
  'revert',
  'style',
  'test'
];
```

## **Scopes:**

- Example commit without specifying scope:
  - `feat: added navigation to React Native app`
- Example commit with specific scope:
  - `feat(lang): added Chinese language support`

1. **Build**: Changes related to the build system or external dependencies. This could include updates to build scripts, package managers, or configuration files.

2. **Chore**: Routine tasks or maintenance that doesn't involve code changes. This could include updating documentation, refactoring code without changing functionality, or organizing files.

   - **Good:** `chore: update dependencies to latest versions`
   - **Less Efficient:** `chore: miscellaneous updates`

3. **CI**: Changes to the continuous integration (CI) configuration or scripts. This includes modifications to the automated build, test, and deployment processes.

   - **Good:** `chore: update dependencies to latest versions`
   - **Less Efficient:** `chore: miscellaneous updates`

4. **Docs**: Updates or additions to documentation, such as README files, API documentation, or inline code comments.

   - **Good:** `docs: add usage instructions to README`
   - **Less Efficient:** `docs: updated documentation`

5. **Feat**: New feature implementations or additions. This represents the introduction of new functionality or significant enhancements to existing features.

   - **Good:** `feat: implement user profile page`
   - **Less Efficient:** `feat: added a new feature`

6. **Fix**: Bug fixes or corrections to existing code or functionality. This type is used when addressing issues or defects.

   - **Good:** `fix: resolve issue with user login`
   - **Less Efficient:** `fix: fixed a problem`

7. **Perf**: Changes aimed at improving performance. This could involve optimizations, code refactoring, or algorithm improvements to enhance the execution speed or efficiency of the code.

   - **Good:** `perf: optimize database queries for faster results`
   - **Less Efficient:** `perf: improved performance`

8. **Refactor**: Code changes that neither fix a bug nor add a feature. Refactoring involves modifying the code structure or design without changing its external behavior. This could include renaming variables, extracting reusable functions, or reorganizing code.

   - **Good:** `refactor: simplify data processing logic`
   - **Less Efficient:** `refactor: made some code changes`

9. **Revert**: Reverting a previous commit. This type is used when reverting or undoing a previous commit's changes.

   - **Good:** `revert: Revert "feat: implement user profile page"`
   - **Less Efficient:** `revert: Undo recent changes`

10. **Style**: Changes related to code style or formatting. This includes whitespace adjustments, formatting improvements, or adhering to coding style guidelines.

    - **Good:** `style: format code for consistency`
    - **Less Efficient:** `style: improved code style`

11. **Test**: Adding or modifying tests. This could involve writing unit tests, integration tests, or updating existing test cases.

    - **Good:** `test: add unit tests for authentication module`
    - **Less Efficient:** `test: testing updates`

12. Breaking Changes
    - **Good:** `breaking change: update API authentication method`
    - **Less Efficient:** `breaking change: important changes made`
