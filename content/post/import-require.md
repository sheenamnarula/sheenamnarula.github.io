+++
title = "Import Vs Require"
subtitle = "This article is about whether to use import or require and why node js still does not support import/export."


# View.
#   1 = List
#   2 = Compact
#   3 = Card
view = 3

+++

Syntax of import/export :

file: exportVar.js
export const m = 1 ;

file: importVar.js
import {m} from exportVar.js

Syntax of require :

file:exportVar.js
const m = 1;
module.exports = m ;

file: importVar.js
const m = require('./exportVar.js')

### Loading Strategy :

Mainly import/export i.e. ES6 structure, involves asynchronous loading of modules.
But in case of require(), synchronous loading of modules takes place.
It means, if a file needs to load 5 modules, in case of ES6 structure, second module won't wait for first module to be loaded completely.But in case of require, loading of second module will start aftee loading of first module is completed.

This is the key difference between import/export and require.

To get more deep in to this, we need to know how ES6 structure is working and how it is different from Common js.

### Working difference :

But a big question is why in node.js ES6 import/export is still not supported if it is good to load modules asynchronously?
