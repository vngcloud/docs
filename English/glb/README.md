# Global Load Balancer

Global Load Balancer (GLB) is a network traffic distribution solution designed for multi-region environments. Unlike traditional Load Balancers that operate only within a single region or local network, GLB can distribute traffic across servers located in multiple geographic regions.

### Why Use GLB? <a href="#tai-sao-nen-su-dung-glb" id="tai-sao-nen-su-dung-glb"></a>

* **Global Reach:** Enables traffic distribution across servers located in different geographic regions.
* **Improved Performance:** Reduces response time by routing user requests to the nearest available server.
* **High Availability:** Minimizes risks and ensures service continuity even if one region experiences failures.
* **Scalability:** Easily add or remove servers from the pool without affecting system operations.
* **Flexibility:** Simplifies the configuration and management of Global Pools, allowing flexible load-balancing adjustments based on demand.
* **Cost Optimization:** Efficiently utilizes server resources by evenly distributing workloads.

### Comparison with Traditional Load Balancer <a href="#so-sanh-voi-load-balancer-truyen-thong" id="so-sanh-voi-load-balancer-truyen-thong"></a>

| Feature            | Traditional LB                     | GLB                                                                    |
| ------------------ | ---------------------------------- | ---------------------------------------------------------------------- |
| Scope of Operation | Within a single VPC network        | Across multiple regions                                                |
| Primary Purpose    | Load balancing within a local area | Multi-region load balancing with optimized performance and reliability |
| Scalability        | Limited                            | Flexible and easy to scale                                             |
| Complexity         | Low                                | Higher, but with more advanced features                                |
