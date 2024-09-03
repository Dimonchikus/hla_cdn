# Custom CDN Setup

This project demonstrates the setup of a custom CDN using Docker, BIND, HAProxy, and Nginx.

## Architecture

- **BIND Server**: Acts as the DNS server to resolve requests to the load balancers.
- **Load Balancer 1**: Distributes traffic between Node 1 and Node 2.
- **Load Balancer 2**: Distributes traffic between Node 3 and Node 4.
- **Nodes (1-4)**: Serve the content (e.g., images) to the users.

## Load Balancing Approaches: Pros and Cons

| **Criteria**      | **Fewest Hops**                                         | **Number of Seconds Away**                                    | **Highest Availability by Performance**                          |
|-------------------|---------------------------------------------------------|---------------------------------------------------------------|------------------------------------------------------------------|
| **Latency**       | **Pros:** Low latency by reducing network hops.         | **Pros:** Prioritizes the lowest latency path to the user.     | **Pros:** Directs traffic to the most responsive server, reducing latency. |
|                   | **Cons:** May not always choose the fastest path due to changing network conditions. | **Cons:** Requires real-time latency measurements, which can fluctuate. | **Cons:** May not always select the closest server, leading to slightly higher latency in some cases. |
| **Complexity**    | **Pros:** Relatively simple to implement.               | **Pros:** Straightforward to configure with existing tools.    | **Pros:** Advanced monitoring provides a comprehensive performance view. |
|                   | **Cons:** Requires consistent monitoring of network paths. | **Cons:** More complex to maintain as it requires continuous measurement of RTT. | **Cons:** High complexity due to the need for continuous performance monitoring and decision-making logic. |
| **Scalability**   | **Pros:** Scales well as additional nodes are added.    | **Pros:** Can handle scaling well if infrastructure supports low-latency connections. | **Pros:** Excellent scalability, as it can adapt to changing loads dynamically. |
|                   | **Cons:** May not adapt well to sudden changes in network topology. | **Cons:** Latency measurements might become less reliable as the network scales. | **Cons:** High demand on resources due to complex monitoring and analysis required. |
| **Reliability**   | **Pros:** Reliable if the network topology is stable.   | **Pros:** Can adapt to network congestion or failure by rerouting traffic. | **Pros:** Ensures that traffic is routed to the most available and responsive servers, improving overall reliability. |
|                   | **Cons:** Network changes can affect performance.       | **Cons:** Fluctuations in latency can lead to inconsistent routing decisions. | **Cons:** Risk of decision-making delays or errors in highly dynamic environments. |
| **Cost**          | **Pros:** Low cost to implement and maintain.           | **Pros:** Moderate cost, depending on the frequency of latency checks. | **Pros:** Can reduce costs related to downtime and poor performance. |
|                   | **Cons:** Potential indirect costs if suboptimal paths lead to slower user experiences. | **Cons:** Increased operational costs due to the need for real-time latency measurements. | **Cons:** Higher costs associated with the need for advanced monitoring tools and more robust infrastructure. |

## Setup Instructions

1. Clone the repository.
2. Start the services using Docker Compose:
   ```bash
   docker-compose up -d
