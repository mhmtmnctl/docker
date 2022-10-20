# Hands-on Docker for Java Devs : Networking 

This hands-on gives a brief understanding of networking among containers

## The Bridge Network
 
 A simple activity on bridge networks

- Check the available networks

    docker network ls

- Start 2 busybox containers named busybox1 and busybox2

    docker run -dit --name busybox1 busybox /bin/sh
    docker run -dit --name busybox2 busybox /bin/sh

- See if the containers are running

    docker ps

- Check and inspect if the containers are attached to the bridge network

    docker network inspect bridge

The result may look similar to this:

[
    {
        "Name": "bridge",
        "Id": "5077a7b25ae67abd46cff0fde160303476c8a9e2e1d52ad01ba2b4bf04acc0e0",
        "Created": "2021-03-05T03:25:58.232446444Z",
        "Scope": "local",
        "Driver": "bridge",
        "EnableIPv6": false,
        "IPAM": {
            "Driver": "default",
            "Options": null,
            "Config": [
                {
                    "Subnet": "172.17.0.0/16",
                    "Gateway": "172.17.0.1"
                }
            ]
        },
        "Internal": false,
        "Attachable": false,
        "Ingress": false,
        "ConfigFrom": {
            "Network": ""
        },
        "ConfigOnly": false,
        "Containers": {
            "7fea140327487b57c3cf31d7502cfaf701e4ea4314621f0c726309e396105885": {
                "Name": "busybox1",
                "EndpointID": "05f216032784786c3315e30b3d54d50a25c1efc7d2030dc664716dda38056326",
                "MacAddress": "02:42:ac:11:00:02",
                "IPv4Address": "172.17.0.2/16",
                "IPv6Address": ""
            },
            "9e6464e82c4ca647b9fb60a85ca25e71370330982ea497d51c1238d073148f63": {
                "Name": "busybox2",
                "EndpointID": "3dcc24e927246c44a2063b5be30b5f5e1787dcd4d53864c6ff2bb3c561519115",
                "MacAddress": "02:42:ac:11:00:03",
                "IPv4Address": "172.17.0.3/16",
                "IPv6Address": ""
            }
        },
        "Options": {
            "com.docker.network.bridge.default_bridge": "true",
            "com.docker.network.bridge.enable_icc": "true",
            "com.docker.network.bridge.enable_ip_masquerade": "true",
            "com.docker.network.bridge.host_binding_ipv4": "0.0.0.0",
            "com.docker.network.bridge.name": "docker0",
            "com.docker.network.driver.mtu": "1500"
        },
        "Labels": {}
    }
]

- See under containers that busybox1 and busybox2 exist.

- Attach to one of the containers

    docker attach busybox1

- check which user is active

    whoami

- check the IPV4 address

    hostname -i

- ping the other container with its IP address.

    ping 172.17.0.3

* So, in this activity, we created 2 containers, they were attached to default bridge network. We entered the containers (machines), then we observed that they could communicate with each other.
