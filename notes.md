michael jackson
unpkg
- cdn for everything on npm
- examples: https://github.com/unpkg/unpkg-demos
- use webpack to add script tags for CDN libs instead of bundling them
    - https://github.com/unpkg/unpkg-demos/blob/master/webpack-react/webpack.config.js
    - https://github.com/mastilver/dynamic-cdn-webpack-plugin
- module level cdn caching
- use https://github.com/systemjs/systemjs to load commonjs modules via web

shirley wu
d3 & react
- react -> rendering; d3 -> calculations
- d3 only needs to render (access dom) for transitions, axes, brushes
- d3 by itself is enough for hover, click, simple interactions
- react for componentizing visualizations & managing state as user interacts
- interaction -> propagate from parent -> data calculation in componentwillreceiveprops / render

Devon Lindsey
A hand wave of React for all your Internet of Thangs
- adafruit pn532 breakout board
- johnny-five.io
- https://unpkg.com/augustctl@0.1.1/
- http://iamdustan.com/react-hardware/

Michael Chan
Back to React: The Story of Two Apps
- shel silverstein missing piece
- jit solutions
- bigger components, inline styles, component state -> don't break out until needed
- know who's driving "what role does react play in your app?"
- do it now / fuck it - don't perf code
- know your patterns: hoc vs callbacks / render funcs
- "it's not the edge that's bleeding, it's you"
    - make it simple until it doesn't work anymore
- "debugging is twice as hard as writing the code, if you write as clever as possible you are by definition unable to debug it"
- partner, don't depend - when you npm install its your code now

Lin Clark
What WebAssembly means for React
- probably not worth it yet but might bring speed gains in future??

Ben Ilegbodu
Layperson's guide to React Fiber
- diffs btwn 15 & 16
    - no React.PropTypes
    - no createClass
    - components can return arrays; <Aux> pattern --
        const Aux = (props) => props.children;
        const SomeComponent = () => (
            <Aux>
                <div>...</div>
                <p>...</p>
            </Aux>
        );
    - components can return strings (i18n)
    - uncaught errors unmount app
    - `componentDidCatch(error, errorInfo)` ('ErrorBoundary' class)
        class ErrorBoundary extends PureComponent {
            state = { hasError: false }
            componentDidCatch(error, info) {...}
            render() {
                if (!this.state.error) { return this.props.children }
            }
        }
- https://github.com/chentsulin/awesome-react-renderer
- node_modules/react-dom/cjs/react-dom.development.js
    - `fiberAsyncScheduling: true`
    - ReactDOM.unstable_deferredUpdates(() => {
        this.setState((state, props) => {
            // return next state
        })
    })
- lin clark: cartoon intro to fiber
- slides: http://www.benmvp.com/slides/2017/reactrally/fiber.html#/

Bonnie Milián
ReacTex: using React Native and Neural Networks to recognize handwritten equations
- deepdreamgenerator.com
- udacity deep learning nanodegree andrew ng
- siraj raval ai edu

Nicolas Gallagher
Twitter Lite, React Native, and Progressive Web Apps
- DOM requires too many abstractions; doesn't handle touch; CSS is hard
- react native = react without DOM
- StyleSheet -> atomic css
- Q: best practice for "media queries" in component based design?
- glitch.com/edit/#!/rnw
- can use same components on native & web; no difference for DOM (i.e., traditional react)
- react-native-web, react-primitives, react-sketchapp

Jana Beck
React-ing htmlFor=empathy
- http://janabeck.com/diving-bell-talk/#/
- https://divingbell.io/

Zack Argyle
Redux + ServiceWorker = Offline React
- ServiceWorker = proxy, cache, push notif., sync
- offline-plugin, sw-precache, workbox, service-workers

8/25
Preethy Kasireddy
We all started somewhere

Evan Czaplicki
Elm - Convergent Evolution
- both have vDOM
- both uni-directional data flow
- elm architecture: model -> html -> elm runtime -> messages (to model)
- react: components + UDDF
- elm: functions = only UDDF
- react: immutable makes it better, but not enforced
- http://swannodette.github.io/2013/12/17/the-future-of-javascript-mvcs
- elm: lazy - keep ref to fn and args, memoize results, dont compare again for rendering
- static analysis: TS/flow vs. built in amazing errors
- noredink: 200k lines of elm, 0 runtime exceptions
- npm vs elm-package: AUTO semantic versioning, elm can detect major changes
- guide.elm-lang.org

Henry Zhu
So how does Babel even work? Let's create the JSX transform to find out!
- http://astexplorer.net/
- babel is independent, just a project (no funding)
- developers <-> babel <-> tc39

Jennifer Van
Scaling My First Enterprise React App!
- enterprise: persist, grow, tested
- scale: things have to stay fast & usable
- how to keep react fast?
    - presentation vs. container component
    - ?react_perf & open devtools
    - remove unnecessary renders: `shouldComponentUpdate`
- how to make app seem fast?
    - prioritize network calls
        - devtools -> network tab -> priority column
    - rendering priority:
        - html
        - css
        - ajax
        - images
        - scripts
        - font
        - <link rel="preload (local) | preconnect (remote)"> for fonts
- how to keep redux fast?
    - setState
    - connect at multiple components
    - normalized state
- how to keep agile cycles fast as dev team grows
    - organize by feature: container, component, ducks
    - docs
    - types!
- how to maintain usability as user base grows?
    - accessibility
    - react-a11y
    - react-axe

Sean Larkin
Everything is a plugin!! Mastering webpack from the inside out
- @TheLarkInn
- tapable instances
    - compiler
        - top level
        - `const compiler = webpack(config);` <- compiler instance
    - compilation: "the brain"
    - resolver: "the blood hound"
    - module factory
        - takes successfully resolved request
        - collects source for file
        - wrap in module object
    - parser
        - module object -> AST
        - find all require/import, create dependency object
        - module -> require/import -> module + dependencies
    - template
        - data bind to view
        - data = code; view = output file (`__webpack_require__(xyz)`)
        - chunk = array of modules (module = file + deps)
- compiler -> compilation -> module -> loader -> parser -> dependencies -> recurse deps as modules

```
return (
    <WriteToDisk render={({ compilation, userConfig}) => (
        compilation.chunks.map(chunk => (
            <Bundle name={chunk.name}>
        ))
    )}>
)
```

- every tapable instance can be plugged in to
- github.com/thelarkinn/everything-is-a-plugin
- npm install
- git checkout 1.0
- webpack.academy
- artsy-webpack-tour
- webpack.js.org/concepts
- contrib: triage, loaders, docs, use
- opencollective.com/webpack

Cameron Matheson
GraphQL IRL
- graphql = types & resolvers
- DataLoader

Justice Mba
Demystifying setState()

David Khourshid
Infinitely Better UIs with Finite Automata
- "bottom up" -> make basic version, iterate
- UI = graph, not tree
- "Deterministic Finite Automata"
    - finite: number of states
    - automata: logical sequence
    - deterministic: given current state & action, next state is deterministic (predictable)
    - AKA "finite state machine"
- initial state + transitions between states; transitions are directed
- common language for designer & developer

ex:
```
const machine = {
    idle: {
        CLICK: 'loading'
    },
    loading: {
        RESOLVE: 'goat'
        REJECT: 'error'
    },
    ...
}

const transition = machine[state][action]
```

- sitoscape (??)
- from each point on graph, use dijkstra to find shortest path to any other point
    - automate unit testing
- caveat: "state explosion" - add a single state adds lots of transitions
- fix: statecharts a.k.a. hierarchical finite state machines
- orthogonal state machines for being in more than one state at a time
- history states
- xstate (on npm)
- constructing the user interface with statecharts - ian horrocks
- statecharts a visual formalism for complex systems - david harel
- pure ui - guillermo rauch
- pure ui control - adam solove
- https://github.com/davidkpiano/xstate

Cara Kuei
Start a conversation between browser windows
- postmessage

Max Stoiber
OSS
- can i make it open source?
- knowledge can be made into open source project (or blog post)
- documentation PRs
