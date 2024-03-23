# API Service

| Category     | SLI | SLO |
|--------------|-----|-------------------------------------------------------------------------------------------------------------|
| Availability | The percentage of time the service is operational and can handle requests over a given period. This can be measured by the ratio of successful responses to the total number of requests. | 99% |
| Latency | The time it takes for a request to be processed and a response to be returned. This is typically measured in milliseconds (ms). | 90% of requests below 100ms |
| Error Budget | The rate of requests that result in an error compared to all requests. Errors can be client-side (4xx HTTP codes) or server-side (5xx HTTP codes). | Error budget is defined at 20%. This means that 20% of the requests can fail and still be within the budget |
| Throughput | The number of requests processed by the service per unit of time. | 5 RPS indicates the application is functioning |