# eslint-lwc-config


This document outlines the code style rules for our Salesforce Lightning Web Components (LWC) and Aura Components projects, using **Allman style** for JavaScript and adapted principles for HTML and CSS. The setup is enforced via ESLint, Prettier, Stylelint, and VS Code, with pre-commit hooks for consistency. Follow these guidelines to ensure readable, maintainable code across the team.

## 1. Overview

We use **Allman style** (BSD style) for JavaScript/TypeScript in LWC/Aura controllers and helpers, characterized by:
- Opening braces on a new line, aligned with the control statement or function.
- Closing braces on a new line, aligned with the opening brace.
- 4-space indentation for code within blocks.
- Consistent use of braces, even for single statements.

For HTML and CSS, we adapt Allman principles with 4-space indentation, clear block separation, and consistent formatting.

**Example (JavaScript)**:
```javascript
import { LightningElement } from 'lwc';

export default class MyComponent extends LightningElement
{
    handleClick(event)
    {
        if (event.target.checked)
        {
            console.log('Clicked');
        }
    }
}
```

**Example (HTML)**:
```html
<template>
    <div class='container'>
        <lightning-card title='My Card'>
            <p slot='body'>Content here</p>
        </lightning-card>
    </div>
</template>
```

**Example (CSS)**:
```css
.container
{
    padding: 16px;
    display: flex;
}
```

## 2. Tooling Setup

We use the following tools to enforce formatting:
- **ESLint**: For JavaScript/TypeScript (Allman style, Salesforce LWC rules).
- **Prettier**: For HTML formatting in LWC/Aura templates.
- **Stylelint**: For CSS formatting in LWC/Aura styles.
- **VS Code**: Primary IDE with extensions for formatting on save.
- **Pre-commit Hooks**: To enforce formatting before commits.
- **Salesforce CLI**: For linting and deployment.

### Prerequisites
- Install **Node.js** (v16 or higher) and `npm`.
- Install **Salesforce CLI** (`sfdx`).
- Install **VS Code** with the **Salesforce Extension Pack** (`salesforce.salesforcedx-vscode`).
- Install VS Code extensions:
  - `dbaeumer.vscode-eslint`
  - `esbenp.prettier-vscode`
  - `stylelint.vscode-stylelint`

## 3. Configuration Files

Place the following configuration files in the project root to enforce Allman style and consistent formatting.

### 3.1 ESLint Configuration (`.eslintrc.json`)
For JavaScript in LWC/Aura controllers and helpers:
```json
{
    "env": {
        "browser": true,
        "es2021": true
    },
    "extends": [
        "plugin:salesforce/recommended",
        "eslint:recommended"
    ],
    "plugins": [
        "salesforce"
    ],
    "rules": {
        "brace-style": ["error", "allman"],
        "indent": ["error", 4],
        "quotes": ["error", "single"],
        "semi": ["error", "always"],
        "comma-dangle": ["error", "never"],
        "space-before-function-paren": ["error", "never"],
        "space-before-blocks": ["error", "never"],
        "linebreak-style": ["error", "unix"],
        "function-paren-newline": ["error", "consistent"],
        "no-multiple-empty-lines": ["error", { "max": 1 }],
        "max-len": ["error", { "code": 120 }]
    }
}
```

**Install Dependencies**:
```bash
npm install --save-dev eslint @salesforce/eslint-config-lwc
```

### 3.2 Prettier Configuration (`.prettierrc`)
For HTML in LWC/Aura templates:
```json
{
    "tabWidth": 4,
    "useTabs": false,
    "singleQuote": true,
    "printWidth": 120,
    "bracketSameLine": false,
    "endOfLine": "lf"
}
```

**Install Dependency**:
```bash
npm install --save-dev prettier
```

### 3.3 Stylelint Configuration (`.stylelintrc.json`)
For CSS in LWC/Aura styles:
```json
{
    "extends": "stylelint-config-standard",
    "rules": {
        "block-opening-brace-newline-before": "always",
        "block-opening-brace-newline-after": "always",
        "block-closing-brace-newline-before": "always",
        "indentation": 4,
        "string-quotes": "single",
        "declaration-block-trailing-semicolon": "always",
        "max-line-length": 120,
        "max-empty-lines": 1,
        "linebreaks": "unix"
    }
}
```

**Install Dependencies**:
```bash
npm install --save-dev stylelint stylelint-config-standard
```

### 3.4 VS Code Settings (`.vscode/settings.json`)
Ensure consistent formatting in VS Code:
```json
{
    "editor.defaultFormatter": "dbaeumer.vscode-eslint",
    "editor.formatOnSave": true,
    "[javascript]": {
        "editor.defaultFormatter": "dbaeumer.vscode-eslint"
    },
    "[html]": {
        "editor.defaultFormatter": "esbenp.prettier-vscode"
    },
    "[css]": {
        "editor.defaultFormatter": "stylelint.vscode-stylelint"
    },
    "editor.tabSize": 4,
    "editor.insertSpaces": true,
    "eslint.format.enable": true,
    "stylelint.validate": ["css"],
    "salesforcedx-vscode-core.push-or-deploy-on-save.enabled": true
}
```

### 3.5 Pre-Commit Hooks (`.pre-commit-config.yaml`)
Automate formatting before commits:
```yaml
repos:
  - repo: https://github.com/pre-commit/mirrors-eslint
    rev: v9.9.0
    hooks:
      - id: eslint
        files: \.(js)$
        args: [--fix]
  - repo:: https://github.com/pre-commit/mirrors-stylelint
    rev: v16.8.1
    hooks:
      - id: stylelint
        files: \.(css)$
        args: [--fix]
  - repo: https://github.com/pre-commit/mirrors-prettier
    rev: v4.0.0-alpha.8
    hooks:
      - id: prettier
        files: \.(html)$
```

**Install Dependency**:
```bash
npm install --save-dev pre-commit
pre-commit install
```

## 4. Setup Instructions

1. **Clone the Repository**:
   - Ensure all configuration files (`.eslintrc.json`, `.prettierrc`, `.stylelintrc.json`, `.vscode/settings.json`, `.pre-commit-config.yaml`) are in the project root.

2. **Install Node.js Dependencies**:
   ```bash
   npm install
   ```

3. **Install VS Code Extensions**:
   - Open VS Code, go to Extensions (`Ctrl+Shift+X` or `Cmd+Shift+X`), and install:
     - `salesforce.salesforcedx-vscode`
     - `dbaeumer.vscode-eslint`
     - `esbenp.prettier-vscode`
     - `stylelint.vscode-stylelint`

4. **Verify Formatting**:
   - Open a JavaScript, HTML, or CSS file.
   - Save the file (`Ctrl+S` or `Cmd+S`) to trigger formatting.
   - Alternatively, use `Alt+Shift+F` to format manually.
   - Check that JavaScript follows Allman style, HTML uses 4-space indentation, and CSS has braces on new lines.

5. **Test Pre-Commit Hooks**:
   - Make changes to a `.js`, `.html`, or `.css` file and commit.
   - Verify that ESLint, Prettier, and Stylelint automatically fix formatting issues.

6. **Integrate with Salesforce CLI**:
   - Run `sfdx force:lint` to check for LWC/Aura-specific issues.
   - Deploy with `sfdx force:source:deploy` to ensure formatted code is pushed to Salesforce.

## 5. Team Guidelines

- **Consistency**: Always commit the configuration files to the repository to ensure all team members use the same settings.
- **Formatting on Save**: Enable `editor.formatOnSave` in VS Code to avoid manual formatting.
- **Resolve Conflicts**: If VS Code extensions conflict (e.g., Prettier overriding ESLint), ensure ESLint is the default formatter for JavaScript (`dbaeumer.vscode-eslint`).
- **SCSS Support**: If using SCSS (based on modular architecture preferences), extend Stylelint:
  ```bash
  npm install --save-dev stylelint-config-standard-scss
  ```
  Update `.stylelintrc.json`:
  ```json
  {
      "extends": "stylelint-config-standard-scss",
      "rules": {
          "block-opening-brace-newline-before": "always",
          "block-opening-brace-newline-after": "always",
          "block-closing-brace-newline-before": "always",
          "indentation": 4,
          "string-quotes": "single",
          "declaration-block-trailing-semicolon": "always",
          "max-line-length": 120,
          "max-empty-lines": 1,
          "linebreaks": "unix"
      }
  }
  ```
  Update `.vscode/settings.json`:
  ```json
  {
      "[scss]": {
          "editor.defaultFormatter": "stylelint.vscode-stylelint"
      },
      "stylelint.validate": ["css", "scss"]
  }
  ```

## 6. Troubleshooting

- **Formatting Not Applied**:
  - Check that the correct formatter is set in `.vscode/settings.json`.
  - Ensure extensions are installed and enabled.
  - Run `eslint --fix`, `stylelint --fix`, or `prettier --write` manually to diagnose issues.
- **Pre-Commit Failures**:
  - View error logs in the terminal when committing.
  - Ensure `pre-commit` is installed (`pre-commit install`).
- **Salesforce-Specific Issues**:
  - Use `sfdx force:lint` to catch LWC/Aura-specific violations.
  - Refer to Salesforce LWC documentation: https://developer.salesforce.com/docs/component-library
- **Performance**: If formatting on save is slow, disable `editor.formatOnSave` and format manually with `Alt+Shift+F`.

## 7. Additional Resources

- **ESLint Rules**: https://eslint.org/docs/rules/
- **Stylelint Rules**: https://stylelint.io/user-guide/rules/
- **Prettier Options**: https://prettier.io/docs/en/options.html
- **Salesforce LWC Style Guide**: https://developer.salesforce.com/docs/component-library/documentation/en/lwc/lwc.create_code_style
- **Allman Style Reference**: https://en.wikipedia.org/wiki/Indentation_style#Allman_style

For questions or updates to this guide, contact the team lead or update this file via pull request.
