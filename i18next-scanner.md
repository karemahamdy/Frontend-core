# Step-by-Step Guide to Using `i18next-scanner`

This guide explains how to set up and use `i18next-scanner` in a React/Next/Vue project to automatically extract text strings and generate translation (i18n JSON) files.

---

## Requirements

* Node.js installed
* A JavaScript/TypeScript project (React, Next.js, Vue, etc.)
* Usage of `t()` or the `useTranslation()` hook in your code

---

## 1. Install the package

In your project root, run:

```bash
npm install i18next-scanner --save-dev
```

> If you use Yarn:

```bash
yarn add i18next-scanner --dev
```

---

## 2. Create a config file

At the root of your project, create a file called `i18next-scanner.config.js` and add the following configuration as a starting point:

```js
export default {
  input: [
    'src/**/*.{js,jsx,ts,tsx,vue}',
    '!**/node_modules/**',
  ],
  output: './locales',
  options: {
    debug: false,
    removeUnusedKeys: true,
    sort: true,
    func: {
      list: ['t'],
      extensions: ['.js', '.jsx', '.ts', '.tsx', '.vue'],
    },
    lngs: ['en', 'ar'],
    defaultLng: 'en',
    defaultNs: 'translation',
    resource: {
      loadPath: 'locales/{{lng}}/{{ns}}.json',
      savePath: 'locales/{{lng}}/{{ns}}.json',
      jsonIndent: 2,
    },
    interpolation: {
      prefix: '{{',
      suffix: '}}',
    },
  },
};
```

### Config notes

* `input`: Defines the paths containing your JSX/TSX/Vue files.
* `func.list`: The function name used for translation (usually `t`).
* `lngs`: Add the languages you want translation files for (e.g., `['en','ar']`).
* `resource.savePath`: Defines where JSON files will be saved.

---

## 3. Adjust for React/Next (optional)

If you use hooks or other helpers, you can extend `func.list`:

```js
func: {
  list: ['t', 'i18n.t'],
},
```

If you use the `Trans` component from `react-i18next`, the scanner can handle it with advanced configuration.

---

## 4. Add a script to `package.json`

Add a script to make running the scanner easy:

```json
"scripts": {
  "i18n:scan": "i18next-scanner -c i18next-scanner.config.js"
}
```

Then run:

```bash
npm run i18n:scan
```

---

## 5. Expected output

After running the command, a `locales` folder will be created or updated with files like:

```
/locales
  /en
    translation.json
  /ar
    translation.json
```

Your `en/translation.json` file will look like:

```json
{
  "Welcome to my app": ""
}
```

Then you can fill the Arabic file:

```json
{
  "Welcome to my app": "مرحبًا بك في تطبيقي"
}
```

---

## 6. Useful options

* **`removeUnusedKeys: true`** → Cleans up unused keys.
* **`sort: true`** → Keeps keys alphabetically sorted.
* **Auto-run** → You can run the scanner before builds or commits using Husky or similar tools.

---

## 7. Optional: Connect to translation management tools

For large projects, use platforms like **Lokalise**, **Crowdin**, or **Locize**. You can export the generated JSON files and upload them for collaborative translation.

---

## 8. Full example: from code to Arabic translation

1. In React code:

```jsx
import { useTranslation } from 'react-i18next';

function Header() {
  const { t } = useTranslation();
  return <h1>{t('Welcome to my app')}</h1>;
}
```

2. Run `npm run i18n:scan` → generates keys in both `en` and `ar` JSON files.

3. Fill the Arabic file:

```json
{
  "Welcome to my app": "مرحبًا بك في تطبيقي"
}
```

4. Switch language in app:

```js
i18n.changeLanguage('ar');
```

---

## 9. Common issues

| Issue              | Solution                                                   |
| ------------------ | ---------------------------------------------------------- |
| **Missing keys**   | Ensure your code uses `t()` or included paths in `input`.  |
| **Duplicate keys** | Use semantic keys like `header.title` instead of raw text. |
| **No output**      | Check `output` path and file permissions.                  |

---

## 10. Advanced steps

* Extract from HTML/Markdown by extending `input` patterns.
* Use Husky to run the scan before each commit.
* Add automatic translation with Google Translate API after scanning.

---

## Conclusion

This guide provides everything you need to start using `i18next-scanner`.
If you’d like, I can:

* Create a config tailored to your project structure.
* Add a Node.js script to auto-translate your JSON files.

Would you like me to add either of those?
