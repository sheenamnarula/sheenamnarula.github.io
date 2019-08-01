+++
title = "Import Vs Require"
featured = true
publishDate = 2019-07-31
subtitle = "This article is about whether to use import or require and why node js still does not support import/export."


# View.
#   1 = List
#   2 = Compact
#   3 = Card
view = 3

+++

#### Syntax of import/export :

file : exportVar.js

```
export const m = 1 ;
```

file : importVar.js

```
import {m} from exportVar.js
```

##### Syntax of require :

file : exportVar.js

```
const m = 1;
module.exports = m ;
```

file: importVar.js

```
const m = require('./exportVar.js')
```

### Loading Strategy :

Mainly import/export i.e. ES6 structure, involves asynchronous loading of modules.
But in case of require(), synchronous loading of modules takes place.
It means, if a file needs to load 5 modules, in case of ES6 structure, second module won't wait for first module to be loaded completely.But in case of require, loading of second module will start after loading of first module is completed.

This is the key difference between import/export and require.

To get more deep in to this, we need to know how ES6 structure is working and how it is different from Common js.

The key difference between the Common JS and ES6 modules is when to know the shape of module.

In Common JS, when a module is exported, the steps performed before execution is given in this figure.

![Example image](/img/common-js-steps.png)

Here the common mistake that most of the developers make in understanding the loading step.
In loading step, it is determined that what kind of thing is pointed by absolute path that is obtained on completion of resolution step.If it is Node.js native module, then dynamic linking of module is decided. On the other hand, if it is JSON file, the content is loaded in memory for further use.
Here is the trick, in wrapper step, before evaluation, the loaded Javasacript is wrapped in a function. For e.g.

In file, example.js

```
const m = 1;
module.exports.m = m;
```

code is actually wrapped and passed to evaluation in below function format :

```
function (exports, require, module, **filename, **dirname) {
const m = 1;
module.exports.m = m;
}
```

Here the exports is a parameter for wrapper function and it is a normal javascript object. So when the wrapper function is evaluated, it returns the exports object which is then used as a result of require(). The main point to note here is that, there is no way to determine as what kind of module is being exported by Common JS until the evaluation of wrapper.

On the other hand, if we use import/export i.e. ES6 feature, the equivalent code of above example is :

In file, example.js

```
export const m = 1;
import {m} from './example.js'
```

In this case, the shape of m is actually determined at the parsing step i.e before evaluation step. Actually, while parsing, and before evaluation, a Module Record is created, where a static listing of modules that have been exported in code are listed and verified. That means, it is verified first whether the exported m exists or not and link between import file and exported module i.e. m is eastablished. Only after creation of this module record, code is actually evaluated.
Here the key point is, before even evaluation of code, the shape of module is known or we can say that, import/export is resolved before evaluation of code.

## Challenge for Node.js :

Here is the challenge for Node.js comes up when exported module is not an ESM i.e ECMASCRIPT Module but a Common JS module because while importing with import statement or according to ES6 structure, shape of module should be known before evaluation but in case of Common JS module it becomes impossible to determine shape of code before evaluation step due to wrapper function.

To resolve this challenge, one proposal came up in which it was proposed that if a module is ESM module, then it will be directly added to list of Module Record but if it is not i.e if it is a Common JS module, then rather than giving error or giving up, the verification step will be left in pending state and a process of evaluation of that module will be executed. After getting confirmation of existence of that module, Module Record will be created.

But again for the implementation of this proposal, Node js requires some mechanism to identify whether the module is ESM or Common JS Module. Various approaches have been suggested but Michael Jackson Script is supposed to be accepted.

### Michael Jackson Script :

In this a new file extension \*.mjs is supposed to be introduced for ESM modules.
Right now, Node is distinguishing between the modules like this :

.node files : native modules

.js : Common JS modules

.json : JSON files

Now \*.mjs will specify that the module is ESM and it should be loaded with the right mechanism.
The key point here is by knowing the extensions of file, loading mechanism will be selected. For Common JS module, evaluation of module will be done first so that verification of existence can be done.

E.g. There are two files common.js and esm.mjs

```
import c from './common.js'
```

will be treated as Common js module

```
import e from './esm.mjs'
```

will be treated as ESM module

## What to do if i want to use ES6 import/export feature in project?

#### Answer is Babel

If we want to use import/export feature of ES6, we need to use babel which transpiles code in Common JS. Here is a point which needs to be understood that Babel only converts the syntax to Common JS syntax so that it can be resolved by Node js, but implementation is according to ESM only.

Example: If we see named imports like

```
import {a,b} from 'ab';
```

This syntax will work only if ab is an ESM. But if it is Common JS module, it is not possible to use this syntax as shape of code can't be determined until evaluation is done in this case.

But here BABEL does a perfect job for us by converting ES6 syntax to Common JS syntax and we get the required implementation.

## Significance of using ES6 structure :

In case of ES6 structure, the first step of loading the contents of file from disk is quite similar but may happen asynchronously. When the content of files is available, they are parsed. While parsing, the shape of exported module is determined and linked to respective import.That means all exports and imports will know their targets before evaluation itself i.e. they are resolved before execution step and that too happen asynchronously.
In node.js terms, we can say that loading scripts, resolution of import and export and evaluation of module code occur over multiple turns of the event loop.

### Practical Example :

module a and b, both does not exist. b is imported using require and a is imported using import. Now due to use of require, existence of b is not verified and code does not throw error for non-existence of b. But in case of module a, existence of a is verified and code throws error for a at very early stage i.e at parsing step only.

![Example image](/img/example-import-require.png)

![Example image](/img/error-import-require.png)
