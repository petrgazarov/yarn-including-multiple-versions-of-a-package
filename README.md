# yarn-including-multiple-versions-of-a-package

### Definition of problem:

Let's say there are two packages named @package-a and @package-b.
@package-b dependends on @package-a.
@package-b's package.json includes:
```
"dependencies": {
  "@package-a": "1.0.0"
}
```
In @package-b's code, @package-a is required like so:
```
const packageA = require('@package-a');
```

I'm using both @package-a and @package-b in my code.
I plan to use multiple versions of each, so I use aliasing to add them by different names.

```
"dependencies": {
  "@package-a-version-1.0.0": "npm:@package-a@1.0.0,
  "@package-b-version-1.0.0": "npm:@package-b@1.0.0,
}
```

In my script, I require @package-b-version-1.0.0 like so:
```
const packageB = require('@package-b-version-1.0.0');
```

And get error:
```
Error: Cannot find module @package-a
```

Looks like yarn did not install @package-a by its original un-aliased name, and @package-b's dependency is not met.

### Expected behavior:

Script should resolve @package-a correctly.

### Steps to reproduce the problem:

1. Clone repo
2. Run `yarn install`
3. Run `yarn start`
