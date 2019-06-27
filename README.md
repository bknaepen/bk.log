Let's see if pages in github could be useful in documenting a few things I learn from day to day...

**Installing Paraview on Ubuntu 18.04** ***(27/06/2019)***

Paraview (http://paraview.org) is a wonderful open-source visualisation software that is designed to explore large datasets produced for example by CFD simulations.

When trying to install and use the current version on an Ubuntu 18.04 LTS system, I encountered several issues that are discribed here.

1) After downloading ParaView-5.6.1-MPI-Linux-64bit.tar.gz, I unpacked it and tried to launch the `paraview` executable. At that stage, I got an error message saying:

```error while loading shared libraries: libOpenGL.so.0: cannot open shared object file: No such file or directory```

This was solved by following [the kind advice ](https://discourse.paraview.org/t/how-to-install-paraview-on-a-remote-server-in-linux/2109) of someone at Kitware on the ParaView support forum. I just needed to also install `libglvnd-dev` and this was done in Ubuntu with `sudo apt-get install libglvnd-dev`.

2) I faced a second issue when trying to launch the `pvserver` on the remote through a terminal window that I had opened on my mac laptop. Upon connecting to the server with the local client, I would get errors on the console,

```
Client connected.
libGL error: No matching fbConfigs or visuals found
libGL error: failed to load driver: swrast
X Error of failed request:  BadValue (integer parameter out of range for operation)
  Major opcode of failed request:  149 (GLX)
  Minor opcode of failed request:  3 (X_GLXCreateContext)
  Value in failed request:  0x0
  Serial number of failed request:  56
  Current serial number in output stream:  57
```

and the client on the mac would quit.

Looking at the documentation (yes this is useful...), I found an option that would also solve this issue and I relaunched the server with,

`./pvserver --disable-xdisplay-test`

From there everything worked fine. Remember also that to run the `pvserver` in parallel, you must install MPI and then launch it with something like,

`mpirun -n 8 ./pvserver --disable-xdisplay-test`








