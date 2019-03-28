# IDT-Fork of conan-libpq

IDT-fork of [conan-libpq](https://github.com/bincrafters/conan-libpq), with OSS fork [here](https://github.com/ilyakrasnovsky/conan-libpq). The rationale is that the pre-uploaded binaries on bincrafters-public-conan for version 9.6.9 of this are only compatible with conan version > 1.8.0, but we are currently on 1.4.5. The right answer is obvious to upgrade our conan infrastructure, but that is pending this [JIRA issue](https://jira.corp.idtus.com:8443/browse/CR-761). 

## Building (CMD.exe)

* `$> C:\Program Files (x86)\Microsoft Visual Studio 12.0\VC\vcvarsall.bat`
* `$> conan create . bincrafters/stable --profile=/some/profile/containing/cmake_installer`

On linux, it's just the latter command, but before you run it, you need to hack conan a little bit: in `venv/lib/python3.5/site-packages/conans/client/tools/net.py`, modify the signature of `def get()` to take in an optional `verify=True`, parameter, and pass that to the `download()` call in the implementation via `verify=verify`. The `conanfile.py` in this directory will then work on Linux. 

See this [procedure](http://gitty.corp.idtus.com/core.low/app-logger/snippets/112) for a similar problem with other Conan libraries. 