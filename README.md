# purescript-faq
An unofficial FAQ for the PureScript language

### What questions would you like to see in an FAQ?

This is a work-in-progress, so please suggest addition questions and/or answers.

### How do I get started?

See the [Getting Started Guide](https://github.com/purescript/documentation/blob/master/guides/Getting-Started.md).

### How do I bundle my app?

The simplest option is with `spago bundle-app`. This produces a single `.js` file that you can execute in `node` or include as a script (for example in your `index.html`). This runs dead-code-elimination, and that added delay is not ideal for quick iterations during development.

Some faster bundling option are:
* Parcel - [example](https://github.com/purescript-halogen/purescript-halogen-template)
* Webpack - [example](https://github.com/milesfrain/tps-save-gist/tree/ace-mode-fixed) (this is more complex than the other examples)
* esbuild - [example](https://github.com/Mateiadrielrafael/purescript-halogen-template)

The bundling process should improve once the PS compiler is modified to output ES modules.

### What are my CSS options?

An [issue tracking the start of a CSS guide](https://github.com/purescript/documentation/issues/336).

### What are some recommended frameworks for frontend web development?

* [Halogen](https://github.com/purescript-halogen/purescript-halogen/) + (optional) [Hooks](https://github.com/thomashoneyman/purescript-halogen-hooks/)
  * [Halogen template](https://github.com/purescript-halogen/purescript-halogen-template/)
* [react-basic](https://github.com/lumihq/purescript-react-basic/)
  * [React basic hooks template](https://github.com/purescript-templates/react-basic-hooks)
* Concur with [React](https://github.com/purescript-concur/purescript-concur-react) or Halogen (in-progress) backend
  * [Concur template](https://github.com/purescript-concur/purescript-concur-starter)

### What are the differences among the above frameworks?

* Halogen is written entirely in PureScript.
* React-basic enables easy interop with the React ecosystem.
* Concur focuses on simple composition of `Widgets`(components).

You may have to dive into the framework docs and look at some examples to get a better sense of the differences.

### What's on the roadmap?

The [Indent to Implement](https://github.com/purescript/purescript/milestone/29) page provides some visibility into items on the todo list, but could be clarified with more details on planned sequence.
Ideally, we'd have a "roadmap summary" page, but until then, here's a short summary:

* 0.13.8 - Current release
* 0.14.0 - Polykinds
  * Currently blocked by coercible bugs
    * https://github.com/purescript/purescript/issues/3875
    * https://github.com/purescript/purescript/issues/3889
* 0.15.0 - ES Modules
  * https://github.com/purescript/purescript/issues/3613

### What's missing from having PureScript 1.0?

* [New package registry](https://github.com/purescript/registry)
* ES6 modules
* Better dead code elimination and bundling
* Complete documentation
* Smooth new-user experience

### Do I need bower to install packages?

No. The docs referring to `bower` are outdated. [Spago](https://github.com/purescript/spago) is is the recommended package management tool.

### Why can't I install a package listed on Pursuit?

[Pursuit](https://pursuit.purescript.org/) lists all published packages, but not all of these make it into the [package set](https://github.com/purescript/package-sets/) accessible to spago. It is encouraged to open PRs to [add these missing packages](https://github.com/purescript/package-sets/blob/master/CONTRIBUTING.md#how-to-add-a-package-to-the-set) to the package set.

You may alternatively consult [Starsuit](https://spacchetti.github.io/starsuit/), which is a Pursuit clone that is synced to the latest package set.

Pursuit plans to be better synced with the new registry.

### What's a good development setup?

A list of available [editor options](https://github.com/purescript/documentation/blob/master/ecosystem/Editor-and-tool-support.md).

Some framework templates also demonstrate how to setup a project with automatic rebuild and webpage refresh upon saving changes:
* [Halogen](https://github.com/purescript-halogen/purescript-halogen-template)
* [React](https://github.com/purescript-templates/react-basic-hooks)

### How does PureScript compare to language X?

There's [a task](https://github.com/purescript/documentation/issues/334) for putting together these summaries. Feel free to contribute.

### How do I write ... ?

The [cookbook](https://github.com/JordanMartinez/purescript-cookbook) aims to provide lots of miscellaneous examples. Feel free to request additional examples.

### Why use `<<<`/`>>>` for function composition, and not `<<`/`>>` (like Elm)?

We chose to match the syntax and capabilities of Haskell's [`Category` class](https://hackage.haskell.org/package/base-4.14.0.0/docs/Control-Category.html#t:Category) (we call it [`Semigroupoid`](https://pursuit.purescript.org/packages/purescript-prelude/docs/Control.Semigroupoid) and drop the identity requirement). Note that `<<<` in PureScript and Haskell allow for composing more than just functions, while `<<` in Elm and `.` in Haskell only work for functions.

Additionally, while not essential, it is common to use `Semigroupoid` composition with operators in the `Functor` hierarchy (eg., `>>=`, `>=>`, `<$>`, `<*>`), and using a three-character operator keeps code in alignment when split over multiple lines.
