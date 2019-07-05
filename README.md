## Linting setup for every project

### Step 1: Install ESLint Config from Airbnb

``https://github.com/airbnb/javascript/tree/master/packages/eslint-config-airbnb``

Install:
``npx install-peerdeps --dev eslint-config-airbnb``

You will be asked to use `yarn` if yarn is your default package manager

Create a file named `.eslintrc` and config like this:
```
{
    "extends": "airbnb",
    "env": {
        "browser": true,
        "node": true
    },
    "rules": {
        "react/jsx-filename-extension": [1, { "extensions": [".js", ".jsx"] }]
    }
}

```

### Step 2: Install and config a code formatter:  `prettier`

``yarn add prettier``

Create a file named  `.prettierrc` and config like this

```
{
    "singleQuote": true,
    "printWidth": 80,
    "editor.formatOnSave": true,
    "proseWrap": "always",
    "tabWidth": 2,
    "requireConfig": false,
    "useTabs": false,
    "trailingComma": "none",
    "bracketSpacing": true,
    "jsxBracketSameLine": false,
    "semi": true
}
```

Now prettier has been setup but not executed (we only `"extends": "airbnb"` up on `.eslintrc` ), we `prettier` to run automagically everytime we `save` a file:

If not existed yet, create a folder named `.vscode` and create a file named `settings.json` and add this line of code in:

```
{
    "editor.formatOnSave": true
}
```

### Step 3: Install and config precommit hooks:  `husky`, and  `lint-staged`

``yarn add husky lint-staged``

In `package.json`, add this config in to run eslint every time you `commit`:

```
"lint-staged": {
    "**/*.js": [
        "eslint --fix",
        "git add"
    ]
},
"husky": {
    "hooks": {
        "pre-commit": "lint-staged"
    }
},
```

We intentionally skip prettier here (because autosaves on step 2 does a better job than on command line, i suffered enough)
