1. Shutdown FortiClient
2. In Windows search, type `msconfig`, go to `Services` tab and uncheck `FortiClient VPN Service Scheduler`. Click apply
3. In Windows search, type `services`, search for `FortiClient VPN Service Scheduler`, on right-click open `Properties`,  check that `Startup type` is either `Manual` or `Disabled`