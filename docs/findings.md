## Findings

In this section, findings from the lab are consolidated by section.

### Probing Vulnerable Services
- The DNS canary captured an outbound lookup after a crafted request was sent to the vulnerable application.
- The callback indicated that malicious input was processed by the application and triggered unexpected external communication.
- This behavior was consistent with the type of unsafe lookup activity associated with Log4Shell.
- The exercise demonstrated that a DNS callback alone can provide enough evidence to flag a service for investigation, validation, and remediation.

### Automating Probes
- Showed how canaries can support automated detection workflows by generating alerts whenever a tokenized resource is accessed or resolved.
- Reinforces how defenders can use canaries as lightweight monitoring controls to detect suspicious behavior at scale without relying only on direct user reporting or manual review.
- The lab also highlighted an important limitation: successful triggering depends on factors such as correct payload formatting, outbound network access, and whether the target application permits the lookup to occur.

### Identifying Illegitimate Access
- The PDF canary demonstrated how document-based tokens can help detect unexpected or unauthorized file access.
- By placing a tokenized document in a shared location, the lab showed how defenders can gain visibility into suspicious interaction with files that should not normally be opened.
- Document canaries remain useful as an early-warning mechanism for identifying possible insider access, unauthorized browsing of shared files, or other suspicious interaction with sensitive content.

### Overall Takeaway

Canary tokens prove to be a useful technical detective measure. Their value comes from providing visibility into suspicious behavior and supporting investigation.





