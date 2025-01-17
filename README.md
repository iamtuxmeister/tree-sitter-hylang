# tree-sitter-hylang

## Status

Subject to change, grammar still evolving.

## Prerequisites

* [emsdk](https://emscripten.org/docs/getting_started/downloads.html#installation-instructions) -- emscripten via homebrew seems to work for macos
* node >= 12 (nvm recommended) -- recently tested 12.9.1, 12,16,1

## Fine Print

* The instructions below assume emsdk has been installed, but `emcc` (tool that can be used to compile to wasm) is not necessarily on one's `PATH`.  If an appropriate `emcc` is on one's `PATH` (e.g. emscripten installed via homebrew), the emsdk steps (e.g. `source ~/src/emsdk/emsdk_env.sh`) below may be ignored.

* `node-gyp` (tool for compiling native addon modules for Node.js) may fail on machines upgraded to macos Catalina. [This document](https://github.com/nodejs/node-gyp/blob/master/macOS_Catalina.md) may help cope with such a situation.

## Initial Setup

Suppose typical development sources are stored under `~/src`.

```
# clone repository
cd ~/src
git clone https://github.com/sogaiu/tree-sitter-hylang
cd tree-sitter-hylang

# create `node_modules` and populate with dependencies
npm install

# create `src` and populate with tree-sitter .c goodness
npx tree-sitter generate

# create `build` and populate with 
npx node-gyp configure

# create `build/Release` and build `tree_sitter_hylang_binding.node`
npx node-gyp rebuild
```

## Grammar Development

Hack on grammar and interactively test.

```
# prepare emsdk (specifically emcc) for building .wasm
source ~/src/emsdk/emsdk_env.sh

# edit grammar.js using some editor

# rebuild tree-sitter stuff and invoke web-ui for interactive testing
npx tree-sitter generate && \
npx node-gyp rebuild && \
npx tree-sitter build-wasm && \
npx tree-sitter web-ui

# in appropriate browser window, paste code in left pane

# examine results in right pane -- can even click on nodes

# find errors and loop back to edit step above...
```

Parse individual files.

```
# create and populate sample code file for parsing named `sample.hy`

# parse sample file
npx tree-sitter parse sample.hy

# examine output similar to web-ui, but less convenient
```

## Measure Performance

```
# single measurement
npx tree-sitter parse --time sample.hy

# mutliple measurements with `multitime`
multitime -n10 -s1 npx tree-sitter parse --time --quiet sample.hy
```

## Build .wasm

Assuming emsdk is installed appropriately under `~/src/emsdk`.

```
# prepare emsdk (specifically emcc) for use
source ~/src/emsdk/emsdk_env.sh

# create `tree-sitter-hylang.wasm`
npx tree-sitter build-wasm
```

## Resources

* [Guide to your first Tree-sitter grammar](https://gist.github.com/Aerijo/df27228d70c633e088b0591b8857eeef)
* [sublime-hylang](https://github.com/tonsky/sublime-hylang)
* [syntax-highlighter](https://github.com/EvgeniyPeshkov/syntax-highlighter)
* [tree-sitter](http://tree-sitter.github.io/tree-sitter/)
* [tree-sitter-hylang.oakmac](https://github.com/oakmac/tree-sitter-hylang)
* [tree-sitter-hylang.SergeevPavel](https://github.com/SergeevPavel/tree-sitter-hylang)
* [tree-sitter-hylang.Tavistock](https://github.com/Tavistock/tree-sitter-hylang)
* [vscode-tree-sitter](https://github.com/georgewfraser/vscode-tree-sitter)
* [web-tree-sitter API](https://github.com/tree-sitter/tree-sitter/blob/master/lib/binding_web/tree-sitter-web.d.ts)

## Acknowledgments

* Aerijo - Guide to your first Tree-sitter grammar
* alehatsman - nvim-treesitter and related discussion
* alexmiller - hylang-related inquiries and docs
* andrewchambers - discussion
* bfredl - neovim and tree-sitter work
* borkdude - analyze-reify, babashka, hy-kondo, edamame, and more
* carocad - parcera and discussions
* clojars - including everyone who has uploaded there
* CoenraadS - Bracket-Pair-Colorizer-2
* EvegeniyPeshkov - syntax-highlighter
* georgewfraser - vscode-tree-sitter
* gfredericks - test.check, generators, and discussions
* GrayJack - discussions and tree-sitter-janet
* hitode909 - vscode-perl-outline
* iarenaza - discussions
* jafingerhut - hylang-related inquiries and haironfire research
* kolja - nrepl-alliance and tree-sitter question concerning HyLang on StackOverflow
* lread - rewrite-hyc and discussions
* mauricioszabo - clover and repl-tooling
* maxbrunsfeld - tree-sitter and related
* monnier - emacs-tree-sitter related
* nwjsmith - tree-sitter upgrade
* oakmac - tree-sitter-hylang.oakmac, conj 2018 unsession, advice, etc.
* pedrorgirardi - discussions, vscode and tree-sitter-hylang bits
* PEZ - calva, vscode tips, and general discussion
* pyrmont - review, error-spotting, fix, and discussions
* rewinfrey - helpful bits from tree-sitter-haskell
* richhickey - hylang, etc.
* Saikyun - discussions
* seancorfield - hylang-related inquiries 
* SergeevPavel - tree-sitter-hylang.SergeevPavel (fork of tree-sitter-hylang.Tavistock with further work)
* SevereOverfl0w - tree-sitter and vim info
* shackra - tree-sitter-query.el
* snoe - discussions
* Tavistock - tree-sitter-hylang.Tavistock
* th0rex - emacs-tree-sitter related
* tobias - clojars work
* tonsky - sublime-hylang work with test data, hylang north talk, alabaster theme
* ubolonton - emacs-tree-sitter
