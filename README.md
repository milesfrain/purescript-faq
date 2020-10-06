# purescript-faq

An unofficial FAQ for the PureScript language.

### What questions would you like to see in an FAQ?

This is a work-in-progress, so please suggest addition questions and/or answers.

### How do I get started?

See the [Getting Started Guide](https://github.com/purescript/documentation/blob/master/guides/Getting-Started.md).

### How do I bundle my app?

The simplest option is with `spago bundle-app`. This produces a single `.js` file that you can execute in `node` or include as a script (for example in your `index.html`). This runs dead code elimination, and that added delay is not ideal for quick iterations during development.

Some faster bundling option are:

- Parcel - [example](https://github.com/purescript-halogen/purescript-halogen-template)
- Webpack - [example](https://github.com/milesfrain/tps-save-gist/tree/ace-mode-fixed) (this is more complex than the other examples)
- esbuild - [example](https://github.com/Mateiadrielrafael/purescript-halogen-template)

The bundling process should improve once the PS compiler is modified to output ES modules.

### What are my CSS options?

An [issue tracking the start of a CSS guide](https://github.com/purescript/documentation/issues/336).

### What are some recommended frameworks for frontend web development?

- [Halogen](https://github.com/purescript-halogen/purescript-halogen/) + (optional) [Hooks](https://github.com/thomashoneyman/purescript-halogen-hooks/)
  - [Halogen template](https://github.com/purescript-halogen/purescript-halogen-template/)
- [react-basic](https://github.com/lumihq/purescript-react-basic/)
  - [React basic hooks template](https://github.com/purescript-templates/react-basic-hooks)
- Concur with [React](https://github.com/purescript-concur/purescript-concur-react) or Halogen (in-progress) backend
  - [Concur template](https://github.com/purescript-concur/purescript-concur-starter)

### What are the differences among the above frameworks?

- Halogen is written entirely in PureScript.
- React-basic enables easy interop with the React ecosystem.
- Concur focuses on simple composition of `Widgets` (components).

You may have to dive into the framework docs and look at some examples to get a better sense of the differences.

### What's on the roadmap?

The [Intended to be Implemented](https://github.com/purescript/purescript/milestone/29) page provides some visibility into items on the todo list, but could be clarified with more details on planned sequence.
Ideally, we'd have a "roadmap summary" page, but until then, here's a short summary:

- 0.13.8 - Current release
- 0.14.0 - Polykinds
  - Currently blocked by coercible bugs
    - https://github.com/purescript/purescript/issues/3875
    - https://github.com/purescript/purescript/issues/3889
- 0.15.0 - ES Modules
  - https://github.com/purescript/purescript/issues/3613

### What's missing from having PureScript 1.0?

- [New package registry](https://github.com/purescript/registry)
- ES6 modules
- Better dead code elimination and bundling
- Complete documentation
- Smooth new-user experience

### Do I need bower to install packages?

No. The docs referring to `bower` are outdated. [Spago](https://github.com/purescript/spago) is the recommended package management tool.

### Why can't I install a package listed on Pursuit?

[Pursuit](https://pursuit.purescript.org/) lists all published packages, but not all of these make it into the [package set](https://github.com/purescript/package-sets/) accessible to spago. It is encouraged to open PRs to [add these missing packages](https://github.com/purescript/package-sets/blob/master/CONTRIBUTING.md#how-to-add-a-package-to-the-set) to the package set.

You may alternatively consult [Starsuit](https://spacchetti.github.io/starsuit/), which is a Pursuit clone that is synced to the latest package set.

Pursuit plans to be better synced with the new registry.

### What's a good development setup?

A list of available [editor options](https://github.com/purescript/documentation/blob/master/ecosystem/Editor-and-tool-support.md).

Some framework templates also demonstrate how to setup a project with automatic rebuild and webpage refresh upon saving changes:

- [Halogen](https://github.com/purescript-halogen/purescript-halogen-template)
- [React](https://github.com/purescript-templates/react-basic-hooks)

### Is there a style guide for PureScript indentation or an autoformatting tool?

Yes. The [`purty` formatter](https://gitlab.com/joneshf/purty/). Note that there are still some [formatting issues](https://gitlab.com/joneshf/purty/-/issues) to fix.

For editor integrations:

- VSCode - [vscode-purty](https://github.com/mvakula/vscode-purty) extension
- Vim/Neovim with coc.nvim - [coc-purty](https://github.com/leighman/coc-purty)

### How does PureScript compare to language X?

There's [a task](https://github.com/purescript/documentation/issues/334) for putting together these summaries. Feel free to contribute.

### How do I write ... ?

The [cookbook](https://github.com/JordanMartinez/purescript-cookbook) aims to provide lots of miscellaneous examples. Feel free to request additional examples.

### Why is there no built-in support for tuples (like Haskell and Elm)?

Records serve the same niche and are more readable. Also, built-in tuples, if added, are one more feature to maintain in the PureScript compiler and one that is easily expressed without built-in support. For example, using [`purescript-tuples`](https://pursuit.purescript.org/packages/purescript-tuples), you can write the following code:

```purs
module Foo where

import Data.Tuple (Tuple(..), (/\), type (/\))

tuple :: Tuple Int String
tuple = Tuple 1 "bar"

-- You can also use `/\` to write tuples
conciseTuple :: Int /\ String
conciseTuple = 1 /\ "bar"
```

Relevant links:

- https://github.com/purescript/documentation/blob/master/language/Differences-from-Haskell.md#tuples
- https://github.com/purescript/purescript/issues/1687

### Why use `<<<`/`>>>` for function composition, and not `<<`/`>>` (like Elm)?

We chose to match the syntax and capabilities of Haskell's [`Category` class](https://hackage.haskell.org/package/base-4.14.0.0/docs/Control-Category.html#t:Category) (we call it [`Semigroupoid`](https://pursuit.purescript.org/packages/purescript-prelude/docs/Control.Semigroupoid) and drop the identity requirement). Note that `<<<` in PureScript and Haskell (in Haskell it's an alias for `.`) allow for composing more than just functions, while `<<` in Elm only works for functions. See [Differences from Haskell](https://github.com/purescript/documentation/blob/master/language/Differences-from-Haskell.md#composition-operator).

Additionally, while not essential, it is common to use `Semigroupoid` composition with operators in the `Functor` hierarchy (eg., `>>=`, `>=>`, `<$>`, `<*>`), and using a three-character operator keeps code in alignment when split over multiple lines.

### If I define an `Ord` instance, why must I also define an `Eq` instance?

Original question:

> For dependent typeclasses (e.g. `Eq` and `Ord`) the operations from one are (always? sometimes?) strictly more powerful than the operations in the other (i.e. you can express `eq` via `compare`). Why is it then that if I define `Ord` for a type, I still need to explicitly define `Eq`? Shouldn't `Eq` be automatically derivable by having an instance of `Ord`?

A seemingly-redundant definition of `Eq` is required to avoid creating [orphan instances](https://github.com/purescript/documentation/blob/master/language/Type-Classes.md#orphan-instances). Imagine if `Ord` and `Eq` were in separate libraries, and the author of the `Ord` library defined an `Ord` instance for some type which didn’t have an `Eq` instance. If instances worked that way, that type would automatically get an `Eq` instance too. Now suppose the author of the `Eq` library adds a direct `Eq` instance for that type which doesn’t agree with the one via `Ord`. What should we do now?
