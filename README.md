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
