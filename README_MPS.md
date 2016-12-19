Gogs fixes:
- SMTP server without password (e.g. Active Directory)


Crosscompile for Windows in linux environment:
- Create user gogs with home
- Download GO to avoid interfering with system's GO
- Export environment variables:
        export GOROOT=$HOME/local/go
        export GOPATH=$HOME/go
        export PATH=$GOROOT/bin:$GOPATH/bin:$PATH
- Install glide in such environment
- Create directory
        mkdir -p $GOPATH/src/github.com/gogits
- Download sources from our branch
        git clone --depth=1 -b m0.9.97 https://github.com/mpindado/gogs
- Install with glide. NOTE: Do not use update!!!! yaml may update other packages and make it all incompatible.
If any package fails, search the commit in the master branch according to the dates and update file glide.lock => If this
file is updated, it must be pushed to this repo.
Execute: glide install
(packages are installed in vendor directory)

- For windows:
GO allows for native cross-compiling, but, if any package uses CGO, it is disallowed by default. For this to work, CGO must be activated
and the gcc crosscompiler must be downloaded: mingw64-gcc, using the right architecture:

CC=x86_64-w64-mingw32-gcc CGO_ENABLED=1 GOOS=windows GOARCH=amd64 go build -tags sqlite

- Once installed, to recompile, simply update the software with git and recompile without touching glide (unless it has changed)
