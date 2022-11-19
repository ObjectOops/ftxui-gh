# Do not use as a template or reference.
ftxui-gh
-------------
Minimal starter project using the [FTXUI library](https://github.com/ArthurSonzogni/ftxui).  
<i>This is a test. Demo.</i>
## Webassembly build:
```bash
cd docs
emcmake cmake ..
make -j 10
```
Visit GH Pages.  
To Do:
- ~~Basic start.~~
- ~~Start with resize.~~ SOLUTION: The resize function for Emscripten isn't available for this version of FTXUI. Commented out that function call.
- ~~With node_modules.~~ SOLUTION: Terminal object must be instantiated with the `allowProposedApi` field set to true. This demo just uses a cache created before that field was required.
- ~~With styles.~~
- ~~Compiler flags.~~ CMAKE
- ~~Final.~~