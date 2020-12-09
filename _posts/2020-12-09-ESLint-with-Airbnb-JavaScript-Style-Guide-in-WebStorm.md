---
excerpt: >-
  How to set up ESLint with Airbnb JavaScript Style Guide in WebStorm
thumb_img_path: '' # images/9.jpg
content_img_path: '' # images/9.jpg
layout: post
---

## Getting started

1. Install `eslint`
```
yarn add eslint --dev
```

2. Setup a configuration file
```
npx eslint --init
```

3. Select as you want
```
$ npx eslint --init
? How would you like to use ESLint? To check syntax, find problems, and enforce code style
? What type of modules does your project use? CommonJS (require/exports)
? Which framework does your project use? None of these
? Does your project use TypeScript? No
? Where does your code run? Browser
? How would you like to define a style for your project? Use a popular style guide
? Which style guide do you want to follow? Airbnb: https://github.com/airbnb/javascript
? What format do you want your config file to be in? JSON
? Would you like to install them now with npm? Yes
```
Automatically install packages below:
```
"eslint-config-airbnb-base": "^14.1.0",
"eslint-plugin-import": "^2.20.2"
```

4. Install `prettier-eslint`
```
"eslint-plugin-prettier": "^3.1.2",
"eslint-config-prettier": "^6.10.1",
"prettier-eslint": "^9.0.1"
```

5. Setup webstorm

```
Preferences - search `eslint` - enable `ESLint`
```

## Resources
* [https://eslint.org/docs/user-guide/getting-started](https://eslint.org/docs/user-guide/getting-started)