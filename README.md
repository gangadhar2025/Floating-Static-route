Static routing is a type of network routing where routes are manually configured by a network administrator. The administrator specifies the exact paths that data packets should take to reach their destination. These routes do not change unless manually modified by the administrator.

A floating static route is a type of backup route in networking that is used only when the primary (preferred) route becomes unavailable.

Primary Route: This is the main route with the lowest administrative distance (AD). The router will use this route for forwarding traffic as long as it is available.

Floating Static Route: This route has a higher administrative distance (usually set manually by the network administrator). The higher AD makes it less preferred than the primary route. The floating static route will not be used unless the primary route fails or becomes unreachable.

ackup Route: The floating static route acts as a backup to the main route.

Higher Administrative Distance: It has a higher AD value than the primary route to make it less preferred.

Automatic Failover: It becomes active only if the primary route fails, ensuring network redundancy and uptime.

Floating static routes are commonly used for:

    Backup internet connections in ISP networks.

    Failover mechanisms in critical systems, ensuring that traffic can be rerouted without manual intervention if a primary route fails.

This makes floating static routes essential for maintaining reliable and uninterrupted connectivity.


🚀 Floating Static Route – Network Redundancy Lab
📌 Project Overview
This project demonstrates Floating Static Routes to implement network redundancy and ensure failover in case of primary link failure. It is designed using GNS3 with Cisco routers and switches to simulate real-world ISP scenarios.

🛠 How It Works
1️⃣ Primary Route Configuration

A standard static route is set with a lower administrative distance (AD), making it the preferred path.

2️⃣ Floating Static Route as Backup

A second static route is configured with a higher AD, ensuring it is only used if the primary route fails.

3️⃣ Automatic Failover

If the primary link goes down, the floating static route activates automatically, maintaining connectivity.

📖 Key Concepts Covered
✅ Static vs Floating Static Routes – Understanding administrative distance (AD) and route preference.
✅ Redundancy & Failover – Ensuring backup connectivity in case of link failure.
✅ Route Verification & Debugging – Using commands like:

sh
Copy
Edit
show ip route  
show ip interface brief  
debug ip routing  
✅ Network Troubleshooting – Diagnosing failures and ensuring proper failover.

⚙️ Lab Setup
🔹 Devices Used in GNS3
4 Routers (R1, R2, R3, R4)

2 Switches

4 PCs (VPCS)

🔹 IP Addressing Scheme
Device	Interface	IP Address
R1	f0/1	192.168.101.1/24
R2	f0/0	192.168.100.1/24
R3	f0/1	192.168.102.1/24
R4	f0/0	192.168.103.2/24
PC1	e0	192.168.10.10/24
PC2	e0	192.168.10.20/24
PC3	e0	192.168.20.10/24
PC4	e0	192.168.20.20/24
🔧 Configuration Steps
1️⃣ Configure Primary Static Route (on R1)
sh
Copy
Edit
ip route 192.168.20.0 255.255.255.0 192.168.100.2 1
This sets the primary route with an administrative distance of 1.

2️⃣ Configure Floating Static Route (on R1)
sh
Copy
Edit
ip route 192.168.20.0 255.255.255.0 192.168.102.2 10
This sets a backup route with an administrative distance of 10. It will activate only if the primary route fails.

3️⃣ Verify Route Selection
sh
Copy
Edit
show ip route
Before failure: The primary route is active.

After failure: The backup route takes over automatically.

🎯 Testing & Verification
1️⃣ Check active routes

sh
Copy
Edit
show ip route
✅ Primary route should be active.

2️⃣ Simulate Link Failure

sh
Copy
Edit
shutdown interface f0/0
✅ Floating static route should take over.

3️⃣ Check Failover Activation

sh
Copy
Edit
show ip route
✅ Backup route should now be active.

📌 Future Enhancements
🔹 Implement IP SLA tracking to make failover more responsive.
🔹 Extend with OSPF/EIGRP for dynamic failover.
🔹 Add load balancing for better traffic management.

