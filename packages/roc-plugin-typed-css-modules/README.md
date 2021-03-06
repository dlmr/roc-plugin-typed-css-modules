# roc-plugin-typed-css-modules
A roc plugin to enable the typed-css-modules, which generates typescript definition
files for your css files.

## How to use?
Install the plugin as a dev dependency in your roc project:
```
npm install --save-dev roc-plugin-typed-css-modules
```

The plugin will now automatically scan any css imports you have in your .ts and
.tsx files and generate d.ts-files for them. **Be aware though that no type
definition files are generated until you reference a style in your css file:**
```
import * as React from 'react';
// It's not enough to just import the style...
import * as styles from './style.scss';

export const MyReactComponent = () => (
// ...you need to reference it as well before the plugin will kick in and generate type definitions!
  <div className={styles.main}>
    <p>Hello CSS Modules world!</p>
  </div>
);
```

Once a reference has been made, the plugin will automatically refresh the type
definitions when you add new styles into your CSS-file.

## Caveats
Currently, the webpack build with roc isn't automatically rerunning after the type
definitions have been generated, which means that the typescript compiler will fail
when trying to compile the file that is referencing the CSS file. Right now, the
solution is unfortunately to rerun the build (or, in development, restart the dev
server).

It also seems necessary to use ES5 as the compile target for the typescript compiler,
or webpack won't be able to pick up the references to the CSS files.

For more on these issues, see [this discussion.](https://github.com/Quramy/typed-css-modules/issues/2)

## Roc documentation
- [Actions](/packages/roc-plugin-typed-css-modules/docs/Actions.md)
- [Commands](/packages/roc-plugin-typed-css-modules/docs/Commands.md)
- [Hooks](/packages/roc-plugin-typed-css-modules/docs/Hooks.md)
- [Settings](/packages/roc-plugin-typed-css-modules/docs/Settings.md)
