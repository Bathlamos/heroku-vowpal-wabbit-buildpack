# Compiling Vowpal Wabbit to update this buildpack
These instructions are valid, as of April 2020 to compile vw version 8.8.1 for Ubuntu
1. Use the Heroku-18 stack: `docker run -it heroku/heroku:18 /bin/bash`.
1. Update apt: `apt update -y`.
1. Install the vw dependencies by following [these instructions](https://github.com/VowpalWabbit/vowpal_wabbit/wiki/Dependencies#ubuntu) for Ubuntu.
   - No need to install Pip, or other optional dependencies
1. Install boost_thread, since it's not in the installation instructions but is stilll needed: `apt install -y libboost-thread-dev`
1. Because the dynamic zlib library (.so) is found instead of the static one, just run the following to force the use of the static library.
   - `rm /usr/lib/x86_64-linux-gnu/libz.so`
   - `ln -s /usr/lib/x86_64-linux-gnu/libz.a /usr/lib/x86_64-linux-gnu/libz.so`
1. Follow instructions [here](https://github.com/VowpalWabbit/vowpal_wabbit/wiki/Building#linux) for building on Linux.
1. Compilation has succeeded. To copy the binary from the Docker container,
   - Run `docker ps` to list active containers
   - Run `docker cp <container-id>:/vowpal_wabbit/build/vowpalwabbit ~/Downloads`