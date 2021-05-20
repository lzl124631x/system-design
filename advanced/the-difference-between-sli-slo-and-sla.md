# The Difference between SLI, SLO, and SLA

The SLA, SLO, and SLI are related concepts though they're different concepts.

* SLA or Service Level Agreement is a contract that the service provider promises customers on service availability, performance, etc.
* SLO or Service Level Objective is a goal that service provider wants to reach.
* SLI or Service Level Indicator is a measurement the service provider uses for the goal.

So here is the relationship. The service provider needs to collect metrics based on SLI, define thresholds of metrics based on SLO, and monitor the thresholds of metrics so that it won't break SLA. In practical, the SLIs are the metrics in the monitoring system; the SLOs are alerting rules, and the SLAs are the numbers of the monitoring metrics applying to the SLOs.

Usually the SLO and the SLA are similar while the SLO is tighter than the SLA. The SLOs are generally used for internal only, and the SLAs are for external. If a service availability violates the SLO, operations need to react quickly to avoid it breaking SLA, otherwise, the company might need to refund some money to customers.

The SLA, SLO, and SLI are based on such assumption that is the service will not be available 100%. Instead, we guarantee that the system will be available greater than a certain number, for example, 99.5%.

The GCP blog [SLOs, SLIs, SLAs, oh my - CRE life lessons](https://cloudplatform.googleblog.com/2017/01/availability-part-deux--CRE-life-lessons.html) explains it a lot. There are also two books heavily rely on these concepts: [Site Reliability Engineering](https://landing.google.com/sre/book.html), and [The Site Reliability Workbook](https://landing.google.com/sre/book.html).

## Example

SLA: the P99 response time is less than 1 second. If I don't meet this, I'll refund you. \(Used externally with the customers\)

SLO: the P99 response time is less than 0.5 second. \(Used internally with the team\).

SLI: the percentile numbers of the response time metric.

## Reference

* [https://enqueuezero.com/the-difference-between-sli-slo-and-sla.html](https://enqueuezero.com/the-difference-between-sli-slo-and-sla.html)

