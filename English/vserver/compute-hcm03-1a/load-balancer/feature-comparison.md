# Feature Comparison

n the dynamic landscape of cloud computing, Load Balancers are essential tools for enhancing application performance and ensuring a seamless user experience. At VNG Cloud, we offer two primary types of Load Balancers: Application Load Balancers (ALBs) and Network Load Balancers (NLBs). This document will help users understand the differences and strengths of these Load Balancer types, enabling them to make informed decisions about which one best suits the requirements of their specific applications.

| Attribute/Feature                 | Application Load Balancer                 | Network Load Balancer                     |
| --------------------------------- | ----------------------------------------- | ----------------------------------------- |
| Layer                             | Layer 7                                   | Layer 4                                   |
| Scheme                            | Internet-facing, Internal                 | Internet-facing, Internal                 |
| Deployment Mode                   | Active/StandBy                            | Active/StandBy                            |
| IAM Permission                    | Full IAM Support                          | Full IAM Support                          |
| **Listener Configurations**       |                                           |                                           |
| Protocol                          | HTTP, HTTPS                               | TCP, UDP                                  |
| Host & Path Routing               | Yes                                       | No                                        |
| HTTP Header-Based Routing         | No                                        | No                                        |
| Server Name Indication (SNI)      | Yes                                       | No                                        |
| Enable Client CA (HTTPS Only)     | Yes                                       | No                                        |
| Timeout                           | Yes                                       | Yes                                       |
| Whitelist IP Source               | Yes                                       | Yes                                       |
| **Pool Configurations**           |                                           |                                           |
| Algorithm                         | Round Robin, Least Connections, Source IP | Round Robin, Least Connections, Source IP |
| Pool Protocol                     | HTTP                                      | TCP, Proxy, UDP                           |
| Enable Sticky Session             | Yes                                       | No                                        |
| Enable TLS encryption             | Yes                                       | No                                        |
| Health Check                      | TCP, HTTP                                 | TCP, HTTP, HTTPS, Ping\&UDP               |
| Target type                       | IP, Instance                              | IP, Instance                              |
| **vMonitor-platform Integration** |                                           |                                           |
| Metric                            | Yes                                       | Yes                                       |
| Audit Log                         | Yes                                       | Yes                                       |
| Access Log                        | Yes                                       | Yes                                       |
