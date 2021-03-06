# ns-3-9-ngwmn
Modifications to ns-3.9 used for the publication of the NGWMN/BWCCA 2010 paper "[Adaptive Mixed Bias Resource Allocation for Wireless Mesh Networks](http://www.computer.org/csdl/proceedings/bwcca/2010/4236/00/4236a622-abs.html)"

Since it has been some time since this code has been compiled - there are few "tweaks" to get it to run correctly in modern Ubuntu (15.10) with the current g++ (4.9.2).

See this link: https://www.nsnam.org/wiki/HOWTO_build_old_versions_of_ns-3_on_newer_compilers

The vanilla unmodified version of ns-3.9 can be downloaded here: https://www.nsnam.org/ns-3-9/

So far I require this to build the simulator: CXXFLAGS="-Wall" ./waf configure --disable-python

### Modifications for compilation in Ubuntu 15.10 ###
In addition, to get it compile I required the following changes:

* In ```src/core/unix-system-wall-clock-ms.cc```, ```src/helper/animation-interface.cc``` and ```utils/test-runner.cc```
  * ```#include <unistd.h>```
* In ```src/common/spectrum-model.h```
  * ```#include <cstddef>```
* In ```src/devices/emu/emu-net-device.cc```
  * ```#include <sys/types.h>```
  * ```#include <unistd.h>```
* In ```src/devices/tap-bridge/tap-bridge.cc```
  * ```#include <sys/types.h>```
  * ```#include <unistd.h>```
* In ```src/devices/wimax/wimax-mac-queue.h```
  * remove the word ```private``` from within the class definition

### Modified to Make the Experiment Work ###
As part of the modifications required to make the code I created work, I had to modify the following files:
* ```src/applications/udp-client-server/udp-server.cc```
* ```src/applications/udp-client-server/udp-server.h```
* ```src/devices/wifi/wifi-mac-queue.h```
* ```src/devices/wifi/wifi-mac-queue.cc```
* ```src/devices/wifi/dca-txop.cc```
* ```src/devices/wifi/dca-txop.h```
* ```src/common/packet.h```
* ```src/common/packet.cc```
* ```src/common/nix-vector.h```
* ```src/common/nix-vector.cc```

### Compiling and Running the Experiment ###
```./waf --run=scratch/ngwmn```

All of the configuration for the simulation is specified in the scratch/ngwmn.cc file.
