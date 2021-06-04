# paloalto-dbl

This contains up-to-date versions of the following IP prefix sources for use as Palo Alto External Dynamic lists. You will need
to bind EDL objects to a GitHub.com SSL profile to enable integration into the firewall.

aws-route53-healthchecks (AWS Route53 health check source addresses)
 - SOURCE: https://ip-ranges.amazonaws.com/ip-ranges.json | jq -r '.prefixes[] | select(.service=="ROUTE53_HEALTHCHECKS") | .ip_prefix'

github-api (GitHub API addresses)
 - SOURCE: https://api.github.com/meta | jq -r '.api[]'
