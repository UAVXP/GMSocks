# GMSocks
Finally a working and well written socket extension for Garrys Mod 13!

**IMPORTANT!** This socket library is non blocking on purpose!

# Download
Grab the binaries from here:
https://github.com/azarus/GMSocks/releases/download/0.1/Release.zip

# Docs

There is only 2 functions for udp and it should be enough for basic networking.

*string UDPReceive(number port, string ip, number bytes = 2048)*
- Retrieves data from a desired address
- Returns nil on failure or the retrieved data.
 
 
*number UDPSend(number port, string ip, string data, number length)*
- Sends data to the desired address
- Returns the number of bytes sent

FOR A COMPLETE EXAMPLE LOOK AT Example.lua:
https://github.com/azarus/GMSocks/blob/master/Example.lua

**Ping <-> Pong example:**
```
require("socks");

local Cfg = {};
Cfg.IP = "123.123.123.123";
Cfg.Port = 1234;

	local data = UDPReceive(Cfg.Port, Cfg.IP);
	
	-- Check if we received anything
	if data == nil then
		return;
	end
	
	-- Read json
	local JSONIn = util.JSONToTable(data);
	
	-- Vertify that the json is valid
	if !JSONIn then
			return;
	end
	
	-- Send pong if we have ping or pong reqests
	if JSONIn.Ping then
			local Query = {};
	   	Query.Pong = true;

		 -- Send the packet
		local packet = util.TableToJSON( Query );
		UDPSend(Cfg.Port, Cfg.IP, packet, string.len(packet) );
  end
```

	
