# Mirrorful + Tailwind + NextJs 


**Step 0:**
Delete your existing .mirrorful folder if it exists because we need to replace it with the latest version

**Step 1:**
Upgrade to latest version of Mirrorful.

```
npm install mirrorful@latest -D # or yarn add mirrorful@latest -D if you use yarn. 
```

**Step 2:**
Rerun mirrorful, as we need to replace your existing `.mirrorful` file in step 3

```
npx mirrorful # or yarn run mirrorful

# you should see:
Running Mirrorful version: 3.1.3
Starting Mirrorful in /Users/zeus/code/my-project.

Visit: http://localhost:5050
```

**Step 3:**
Go to  `http://localhost:5050` and in mirrorful, click “I have a theme”.

Add your new colors. For example, you can add supafan-green: `#0c9e09`

**Step 4:**

Export out your config (by clicking on the blue export config button in top right corner), this should replace your .mirrorful folder. Close the pop up.

**Step 5:**
In the `.mirrorful/theme.js` file, rewrite the first line to be the following: (we’ll automate all this in the future)

```javascript
exports.Tokens = { } # instead of export const Tokens = { } 
```

As a sanity check, your .mirrorful/theme.js file should look like this:

```javascript
exports.Tokens = {
  "supafan-green": {
    500: "#0c9e09",
    base: "#0c9e09",
  },
  fontSizes: {
    sm: "1rem",
    md: "1.2rem",
    lg: "1.4rem",
  },
};
```

**Step 6:**

In your tailwind config file add this as your first line. Import your mirrorful theme and add your colors

```javascript
const mirrorful = require('./.mirrorful/theme.js') // THIS LINE IS NEW!

/** @type {import('tailwindcss').Config} */
module.exports = {
  content: [
    './app/**/*.{js,ts,jsx,tsx}',
    './pages/**/*.{js,ts,jsx,tsx}',
    './components/**/*.{js,ts,jsx,tsx}',

    // Or if using `src` directory:
    './src/**/*.{js,ts,jsx,tsx}',
  ],
  theme: {
    extend: {
      colors: mirrorful.Tokens, // THIS LINE IS ALSO NEW! the rest of your file may look different
    },
  },
  plugins: [],
}
```

**Step 7:**
You can use your custom colors in now in your app! Ensure you use a shade, i.e., 500 that exists. For example,

```html
        <h2 className="text-supafan-green-500">
          This uses Tailwind + Mirrorful. Custom Supafan Green Color!
        </h2> 
```
