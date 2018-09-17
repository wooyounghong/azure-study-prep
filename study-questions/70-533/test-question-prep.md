# Implementing Microsoft Azure Infrastructure Solutions

1. You manage a cloud service that supports features hosted by two instances of an Azure virtual machine (VM). 
    You discover that occasional outages causes your service to fail.
    You need to minimize the impact of outages to your cloud service.
    Which two actions should you perform? Each correct answer presents part of the solution.
    + Configure Load Balancing on the VMs.
        - Load Balancer
            * efficiently distributing incoming network traffic across a group of backend servers (server farm or server pool)
            * a public Load Balancer can provide outbound connections for Virtual Machines inside your virtual network by translating private IP address to public IP address
            * acts as the “traffic cop” sitting in front of your servers and routing client requests across all servers capable of fulfilling those requests in a manner that maximizes speed and capacity utilization and ensures that no one server is overworked, which could degrade performance. If a single server goes down, the load balancer redirects traffic to the remaining online servers. When a new server is added to the server group, the load balancer automatically starts to send requests to it.
        - Azure Load Balancer
            * Load-Balance incoming internet traffic to your VMs. This configuration is known as Public Load Balancer
                - Public Load Balancer =  maps the public IP address and port number of incoming traffic to the private IP address and port number of the VM, and vice versa for the response traffic from the VM.
    
    -- SRC: https://www.digitalocean.com/community/tutorials/what-is-load-balancing
            
        
    + Configure VMs to belong to an Availability Set.
    
