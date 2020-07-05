# BuildTools-For-Travis
This repo can be used to run BuildTools and install NMS CraftBukkit versions to the local Maven repo.

It will also cache each version and only run BuildTools for missing versions.

## How to use
1. Copy the BuildTools folder that contains build.sh and place it into your root directory

2. Select the BuildTool versions your NMS code requires from the [BuildTools version page](https://www.spigotmc.org/wiki/buildtools/#versions). For example the default versions in this project are 1.16.1, 1.15.2 and 1.14.4.

3. After you have selected your versions they need to be added to the build.sh file into the array at the top of the script as follows:

```bash
######################################################################
# Add your CraftBukkit versions here how BuildTools would recognise them!
array=("1.16.1" "1.15.2" "1.14.4")
######################################################################
```

4. The final step is to add the following to your travis.yml (Or just base your travis file off of the one provided)
```yml
#This checks if each CraftBukkit version added into 'BuildTools/build.sh' is cached and if not uses BuildTools to install it.
before_install:
- cd BuildTools
- bash build.sh
- cd ../

#Cache the Maven local repo
cache:
  directories:
  - $HOME/.m2
```

This enables the use of NMS code in travis whilst also preventing extremely long build times due to BuildTools after caching.

The initial build of this project takes ~ [11 minutes](https://travis-ci.com/github/JamesPeters98/BuildTools-For-Travis/builds/174323317).
The second build after caching takes ~ [40 seconds](https://travis-ci.com/github/JamesPeters98/BuildTools-For-Travis/builds/174323677)
