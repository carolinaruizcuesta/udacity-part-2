# API Service

| Category     | SLI                                                                | SLO                                                                                                         |
|--------------|--------------------------------------------------------------------|-------------------------------------------------------------------------------------------------------------|
| Availability | (total number of successfull requets) / (total number of requests) | 99%                                                                                                         |
| Latency      | 90th percentile latency over a 5 min period                        | 90% of requests below 100ms                                                                                 |
| Error Budget | (number of error requests) / (total number of requests in budget)  | Error budget is defined at 20%. This means that 20% of the requests can fail and still be within the budget |
| Throughput   | requests per second over a 5 min period                            | 5 RPS indicates the application is functioning                                                              |
