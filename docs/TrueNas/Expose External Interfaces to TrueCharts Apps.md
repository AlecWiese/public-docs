#TrueNas #truecharts #Networking 

Sometimes I need to expose an additional external (outside of the kubernetes cluster) network interface for a Truecharts app. For Example, needing to expose the app to a subnet it doesn't otherwise have access to. to simplify network when rules to allow connections between VLANs cause, or at least appear to cause issues.

Under Service's Port(s) Configuration -> Main Service Port Configuration check the box to enable Expert Config.

1. Click The **Add** Button next to **Add External Interface**
2. Select your Host interface (bridge or ethernet port this connection will run on) i.e **`br1`** or **`eth0`**
3. Under IP **Address Management** -> IPAM Type Select **Use Static IP**
4. Click The **Add** Button next to **Static IP Addresses**
5. Configure your Static IP i.e. **`10.0.10.145/24`**
6. Click The **Add** Button next to **Static Routes**
	Destination: **`0.0.0.0`**
	Gateway: `<Subnet Gateway>`  i.e. **`10.0.10.1`**

Example Screenshot:  
![[External_interface_Truecharts_Example_1.png]]