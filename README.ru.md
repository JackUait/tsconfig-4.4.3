Переводы: [🇺🇸 Английский](README.md)

Этот репозиторий используется в качестве шаблона для первоначальной настройки прекрасно типизированных приложений на React + Next.js + Typescript.

### Прочитайте перед использованием:

В данной конфигурации target (во что будет скомпилирован TS код) выставлен в ES2017 по следующим причинам:

1. Microsoft предлагает использовать ES6+ в [TSConfig Reference](https://www.typescriptlang.org/tsconfig#target) и на это есть свои причины.
2. Единственный браузер, не имеющий поддержки ES8 (ES2017) (а также ES7 (ES2016) и ES6 (ES2015)) это [IE11](https://caniuse.com/es6).
3. [Согласно информации из официального репозитория TS:](https://github.com/Microsoft/TypeScript/wiki/TypeScript-Design-Goals#non-goals) команда TypeScript не ставит перед собой цель "агрессивной оптимизации производительности программ во время выполнения". Это означает, что часть кода скомпилированного в ES5 может иметь более высокую сложность (подразумевается сложность алгоритма по времени и памяти т.е. с точки зрения большого O) чем та, которую вы закладывали в алгоритм изначально. TypeScript может усложнять вашу программу намеренно, для того, чтобы удостовериться, что код отрабатывает одинаково во всех окружениях (браузерах).
4. [TS код скомпилированный в ES5 по всем правилам](https://www.typescriptlang.org/tsconfig#downlevelIteration) (используя флаг downlevelIteration, который учитывает все крайние случаи при компиляции) занимает больше места и следовательно требует больше времени на то, чтобы браузеры могли его интерпретировать. Следовательно, добавляя поддержку IE11 мы ухудшаем UX для тех пользователей, которые используют слабые Android смартфоны или устаревшие iOS устройства.
5. Многие библиотеки, которыми мы с вами пользуемся каждый день, уже отказались от поддержки IE11. Вот несколько из них: [Chakra UI](https://github.com/chakra-ui/chakra-ui/pull/2762#issuecomment-753606667), [Material UI](https://mui.com/ru/getting-started/supported-platforms/) и [Framer Motion](https://github.com/framer/motion/issues/364#issuecomment-542254887).
6. Все современные браузеры (Edge, Safari, Chrome, Firefox, Opera и Safari для iOS) уже поддерживают все фичи пришедшие в язык со спецификациями [ES6 (ES2015)](https://caniuse.com/es6), [ES7 (2016)](https://caniuse.com/sr_es7) и [ES8 (2017).](https://caniuse.com/async-functions,object-values,object-entries,mdn-javascript_builtins_object_getownpropertydescriptors,pad-start-end,mdn-javascript_grammar_trailing_commas_trailing_commas_in_functions)

`Так что поддерживать IE11 в 2021 году почти бессмысленно.`

P.S.
При желании, вы даже можете установить ES9(ES2018) как цель для компиляции в tsconfig.json, но в таком случае нужно учитывать, что Safari до сих пор [не поддерживает часть нового функционала](https://caniuse.com/?feats=mdn-javascript_builtins_regexp_dotall,mdn-javascript_builtins_regexp_lookbehind_assertion,mdn-javascript_builtins_regexp_named_capture_groups,mdn-javascript_builtins_regexp_property_escapes,mdn-javascript_builtins_symbol_asynciterator,mdn-javascript_functions_method_definitions_async_generator_methods,mdn-javascript_grammar_template_literals_template_literal_revision,mdn-javascript_operators_destructuring_rest_in_objects,mdn-javascript_operators_spread_spread_in_destructuring,promise-finally) связанного c регулярными выражениями, который был представлен в этой версии ECMAScript. Даже если вы уверены, что не будете использовать ни одну из функций представленных в этой спецификации, другие библиотеки в вашем проекте могут использовать этот функционал, и в таком случае, вы рискуете потратить огромное количество времени в попытках разобраться чем была вызвана ошибка.
