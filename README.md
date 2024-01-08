# First post

1. **Optimize Regex Usage in PostCSS**

   - **What:** A costly regex operation in `postcss-custom-properties` plugin was taking 4.6s due to serialization and repeated regex over short strings.
   - **Why:** Regex matching against many short strings is slower and incurs serialization costs compared to longer strings.
   - **How:** Implement a check to avoid unnecessary regex operations when the file doesn't contain relevant comments, thereby reducing build time significantly.

2. **Improve SVG Compression in SVGO**

   - **What:** The `strongRound` function in SVGO was inefficient due to casting between string and number types.
   - **Why:** Frequent type casting increases computation time and can trigger garbage collection.
   - **How:** Rewrite the `strongRound` function to avoid string casting and stay in number-land, leading to a 1.4s improvement in build times.

3. **Avoid Unnecessary Recursion and Transpilation in SVGO and @vanilla-extract/css**
   - **What:** Inefficient recursion in SVGO's `perItem` function and problematic transpilation of `for...of` in @vanilla-extract/css.
   - **Why:** Inner functions are hard to optimize, and transpilation can introduce inefficiencies.
   - **How:** Refactor `perItem` to avoid inner functions and patch `for...of` loop in the local `node_modules` to improve performance.

# Second post

From the second post on Node.js performance optimization, here are the key practical takeaways:

1. **Optimize Error Handling in File Checking**

   - **What:** The `isFile` function in Node.js was inefficiently using `fs.statSync()` to check file existence, causing unnecessary error handling overhead.
   - **Why:** The function often threw and caught errors for non-existing files, which was an expensive operation.
   - **How:** Use the `throwIfNoEntry: false` option with `fs.statSync()` to avoid throwing errors for non-existent files, significantly reducing unnecessary overhead.

2. **Implement Caching in Module Resolution**

   - **What:** High frequency of file system checks during module resolution.
   - **Why:** Each module resolution involved multiple file system checks, significantly slowing down the process.
   - **How:** Introduce caching for resolved modules to minimize redundant file system checks, leading to a substantial reduction in linting and testing times.

3. **Reduce File System Calls and Upwards Traversal**
   - **What:** Excessive file system calls and directory traversal during module resolution.
   - **Why:** Resolving modules involved checking multiple directories and file extensions, resulting in a high number of file system calls.
   - **How:** Limit the number of directories and file extensions checked during module resolution and cache the results to prevent repeated checks.
