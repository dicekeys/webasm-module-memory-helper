# Webasm Module Memory Helper

This module addresses some shortcomings of emscripten-compiled modules.

1) It returns a true promise which resolves when the module is loaded and the web assembly is compiled.  This is needed because, until very recently, emscripted modules implemented then but were not true promises.  If you awaited the the promise, your code would enter [an infinite loop](https://github.com/emscripten-core/emscripten/issues/5820).  This module prevents ensures you get a real promise back.
2) This module provides functions that allocate memory within the web assembly module's memory space (where the web assembly code can access it), call a callback you provide with that memory, and clean up that memory when your callback completes.
3) This module provides TypeScript typings so that your compiler will alert you if you're passing a pointer into the memory of one web assembly module to a different web assembly module.
