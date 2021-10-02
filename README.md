Translations: [🇷🇺 Russian](README.ru.md)

I use this repo as a go-to reference for initializing new awesomely typed React + Next.js + TypeScript projects.

### Important note:

This configuration uses ES2017 as the target for tsc for the reasons listed below:

1. Microsoft suggests to use ES6+ in their [TSConfig Reference](https://www.typescriptlang.org/tsconfig#target) and there are reasons for that.
2. The only browser that doesn't have support of ES8 (ES2017) (and also ES7 (ES2016) and ES6 (ES2015)) nowadays is [IE11](https://caniuse.com/es6).
3. [According to the official TS repo](https://github.com/Microsoft/TypeScript/wiki/TypeScript-Design-Goals#non-goals) the TypeScript has no goal to "aggressively optimize the runtime performance of programs". Therefore some of the code compiled to ES5 may be more complex (in terms of time and space complexity) than you would expect. TypeScript does that just to ensure that compiled code will run correctly in any given environment (browser).
4. [TS code properly compiled to ES5 (using downlevelIteration flag that considers all edge-cases)](https://www.typescriptlang.org/tsconfig#downlevelIteration) takes up more space and therefore requires more time to be interpreted by the browser. Therefore by supporting IE11 nowadays we deteriorating UX of the users using low-performance devices as cheap Android smartphones or old iOS gadgets.
5. Some libraries that I as well as many developers all over the world use on a daily basis have already dropped out support for IE11, some good examples are [Chakra UI](https://github.com/chakra-ui/chakra-ui/pull/2762#issuecomment-753606667), [Material UI](https://mui.com/ru/getting-started/supported-platforms/) and [Framer Motion](https://github.com/framer/motion/issues/364#issuecomment-542254887).
6. All modern browsers (Edge, Safari, Chrome, Firefox, Opera and iOS Safari) already support all features presented in [ES6 (ES2015)](https://caniuse.com/es6), [ES7 (2016)](https://caniuse.com/sr_es7) and [ES8 (2017)](https://caniuse.com/async-functions,object-values,object-entries,mdn-javascript_builtins_object_getownpropertydescriptors,pad-start-end,mdn-javascript_grammar_trailing_commas_trailing_commas_in_functions)

`So it makes almost no sense to support IE11 in 2021.`

P.S.
You may go even further and set ES9 (ES2018) as the compile target in tsconfig.json but I wouldn't recommend doing that as Safari [still missing](https://caniuse.com/?feats=mdn-javascript_builtins_regexp_dotall,mdn-javascript_builtins_regexp_lookbehind_assertion,mdn-javascript_builtins_regexp_named_capture_groups,mdn-javascript_builtins_regexp_property_escapes,mdn-javascript_builtins_symbol_asynciterator,mdn-javascript_functions_method_definitions_async_generator_methods,mdn-javascript_grammar_template_literals_template_literal_revision,mdn-javascript_operators_destructuring_rest_in_objects,mdn-javascript_operators_spread_spread_in_destructuring,promise-finally) support for some of new RegExp functionality presented in this version of ECMAScript. Even if you are not going to use any of these functions they might be used internally by one of the libraries you are using in your project. And then you are going to have hard time debugging.
