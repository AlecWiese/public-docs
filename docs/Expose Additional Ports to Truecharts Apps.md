#TrueNas #truecharts #Networking 

When configuring an App in in TrueNas Scale, I sometimes need to expose additional ports for subservices in the container. i.e. exposing a port for homekit in the [Scrypted](https://www.scrypted.app/) [Chart](https://artifacthub.io/packages/helm/truecharts/scrypted) 

First You'll need to configure an External Interface, you can follow this [KB](obsidian://open?vault=Knowledge%20Base&file=Documentation%2FExpose%20External%20Interfaces%20to%20TrueCharts%20Apps) on how.

1. With your IP configured, Navigate to **Add Manual Custom Services** click **Add**
	Name: `<servicename>`
	Service Type: LoadBalancer (Expose Ports) *Default*
	LoadBalancer IP: `<blank>`
2. Click The **Add** Button next to **Additional Service Ports**
	Port Name: `<servicename>`
	Port Type: `<Port Type>`
	Target Port: `<Port>`
	Container Port:`<Port>`
		Note you can configure a different *target* port to expose than the *container* port, as needed. 

**Example Image**
![[Additional_Ports_Truecharts_Example_1.png]]