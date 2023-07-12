# Local lib not found by :local/root
[Post on clojureverse](https://clojureverse.org/t/local-lib-not-found-by-local-root/10174/1)

Regarding [Using local libraries](https://clojure.org/guides/deps_and_cli)

The tree is essentially what is shown in that section:

├── time-lib  
│   ├── deps.edn  
│   └── src  
│       └── hello_time.clj  
└── hello-world  
    ├── deps.edn  
    └── src  
        └── hello.clj  
        
The problem is running hello.clj from hello-world, gives an error saying the java-time library pointed to in time-lib/deps.edn cannot be found, because hello-world/deps.edn which points to it via :local/root ../time-lib doesn't seem to work.

There is a copy of hello.clj in time-lib/src/ as well, just to make sure the java-time library can be found (it doesn't go through the hello-world/deps.edn). Also, we have:

├── nolib  
│   ├── deps.edn  
│   └── src  
│       └── sayhello.clj  

which is just another test to make sure java-time could be found (nolib/deps.edn and time-lib/deps.edn are the same file). It has nothing to do with what the Using local libraries instructions are.

**Solved!**

The problem was solved by Sean Corfield who wondered if I had a :deps in the global deps.edn file referring to the earlier version. That :deps takes priority over the other deps.edn files and so, we were looking for v1.2.0, but the global file kept giving v0.3.2 and resulted in the error.

The problem didn't exist when we didn't have a local deps asking for v1.2.0 directly, but if a local deps asks another local deps, it seems to get overriden by the global deps.

Sean also emphasized that we shouldn't use :deps in the global deps.edn file!
