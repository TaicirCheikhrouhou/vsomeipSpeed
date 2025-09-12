This project demonstrates a vsomeip-based communication setup using SOME/IP protocol for automotive applications. It includes a server and two clients interacting over a network with network namespaces to simulate distributed nodes.
Overview
Server (ns0, 192.168.0.1): Provides svc_SpeedValue (service 0x1234, instance 0x0001) with a method and event for speed data.
5Client1 (ns1, 192.168.0.2): Consumes services from the server and Client2, processes speed data, and sends results back.
Client2 (ns2, 192.168.0.3): Provides svc_SpeedRequest (service 0x5678, instance 0x0001) to respond with RPM data.

Prerequisites
Linux environment with ip netns and veth interfaces.
vsomeip library (v3.5.3) installed at ........
tcpdump and Wireshark for network monitoring.

Setup
Network Configuration:
Three namespaces: server-ns (192.168.0.1), client1-ns (192.168.0.2), client2-ns (192.168.0.3).
Virtual Ethernet pairs: veth0–veth3.
Multicast enabled for 224.244.224.245:30490.
Running the Application
Start Server:
sudo ip netns exec ns0 bash -c 'LD_LIBRARY_PATH=.............. 
                                    VSOMEIP_CONFIGURATION=......... 
                                    VSOMEIP_APPLICATION_NAME=server VSOMEIP_LOCAL_ENDPOINT_DISABLE=1 ./bin/server_main --log-level debug'
Start Client1:
sudo ip netns exec ns1 bash -c 'LD_LIBRARY_PATH=.............
                                    VSOMEIP_CONFIGURATION=...........
                                    VSOMEIP_APPLICATION_NAME=client1 VSOMEIP_LOCAL_ENDPOINT_DISABLE=1 ./bin/client1_main --log-level debug'
Start Client2:
sudo ip netns exec ns2 bash -c 'LD_LIBRARY_PATH=.............
                                    VSOMEIP_CONFIGURATION=...............
                                    VSOMEIP_APPLICATION_NAME=client2 VSOMEIP_LOCAL_ENDPOINT_DISABLE=1 ./bin/client2_main --log-level debug'
Troubleshooting:
Ensure no default configurations in /etc/vsomeip/.
Verify network connectivity with ping and nc.
Check logs for UDS usage or connection errors.
