# Lessons Learned

For each section of this lab, there are key takeaways to dicuss.

## Probing Vulnerable Services

CanaryTokens created a random DNS name. Under normal circumstances, nothing should be querying this DNS record. However, when the exploit was run, the remote server issued a DNS request to resolve the token domain.

While DNS requests are somewhat harmless, this tells us that we can instruct the server to run somewhat arbitrary instructions. The real risk with Log4Shell was that it wasn’t just limited to DNS lookups. It also permitted LDAP requests. Researchers found that using a malicious LDAP server, they could get Log4J instances to load additional Java classes, and in some implementations, this attack chain yielded interactive shells with privileged accounts.

Defenders don’t need to verify the entire exploit path. Successful DNS-based canaries like the one we just used can provide sufficient evidence that a system or service is at risk. Defenders must also be aware of the limits of canaries. This one requires that the remote system have Internet access. A blocked connection could lead to false positives. It’s also important to run tests against known-vulnerable systems to ensure that the test string works as expected. Improperly formatting test strings can also result in false positives.

## Note on Automating Probes: Further Investigation

Attackers find creative ways to bypass pattern matching rules. This [CloudFlare Blog](https://blog.cloudflare.com/actual-cve-2021-44228-payloads-captured-in-the-wild/) is useful to look at some of the additional methods used to manipulate the executable string as observed by Cloudflare.

## Identifying Illegitimate Access

In our action sequence and this lab case, it is possible that someone who is snooping around just click block in this case – effectively defeating the token mechanism. However, checking out the trust settings in Acrobat allows us to see how organizations deal with this. In large organizations, IT departments often manipulate these trust settings to permit access to links from specific trusted domains. Additionally, they can ensure that the default file handler is the preferred application (e.g. Acrobat). We can adjust the trust settings to make the PDF launch without the warning.
