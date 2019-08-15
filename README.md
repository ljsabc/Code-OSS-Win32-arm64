HOW TO BUILD
----

This is a simple instruction on the build step of Code - OSS for Windows ARM64 PCs.

## Requirements

+  Electron v6-0-x (simply use gclient to checkout both the Chromium and the Electron source)
+  Chromium 76.0.3309.118
+  Code-OSS branch electron 6.0.x
+  VS 2019 and its build tools


## Notes

I dont want to push or fork so I will only note some key issues:

### Electron / Chromium

For VS2019, you need to specify /std:c++17 for all projects and suppress some warnings like microsoft-spec. Electron is strictly built against chrome 76.0.3309.118 so you may not want to checkout other versions.
If you have any experiences with a chromium build you will find it quite straightforward.

As chrome 76 is considered an "old" version of chrome, you may need the correct gn.exe. Fortunately, I have prepared that for you.


### Node 

If you dont want to build electron from scratch you can jump to this section. 

With electon and its libraries, all of the projects can be cross-compiled because the node runtime is actually inside the Electron main executable. So you do not need to build Node once again. Once you set the msvs_version and target cpu you can build all of the native node_modules.
Note that some of the node_modules may not compile due to the bump of v8 version. You may simply replace these requirements with my forked repos.

Still, when node-gyp propmts that the v6.0.1 arm64 lib is missing (because electron does not prepare that for us), just place the prebuilt node.lib in the "arm64" sub-folder inside the node-gyp cache. The automatically downloaded header is suitable for build.  


### VSCode

Do not build VSCode with native ARM64 node. It looks like tsc does not work well with the current Node binary. Please always do a cross compile.
For other things just do a yarn and npm compile.   
