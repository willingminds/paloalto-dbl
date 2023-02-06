# paloalto-dbl

This contains up-to-date versions of the following IP prefix sources for use as Palo Alto External Dynamic lists. You will need
to bind EDL objects to a GitHub.com SSL profile to enable integration into the firewall.

- aws-route53-healthchecks (AWS Route53 health check source addresses)

```
 SOURCE: https://ip-ranges.amazonaws.com/ip-ranges.json 
EXTRACT: jq -r '.prefixes[] | select(.service=="ROUTE53_HEALTHCHECKS") | .ip_prefix'
```

- okta (Okta cell addresses)

```
 SOURCE: https://s3.amazonaws.com/okta-ip-ranges/ip_ranges.json
  CELL:
    apac_cell_1
    apac_cell_2
    emea_cell_1
    emea_cell_2
    us_cell_1
    us_cell_10
    us_cell_11
    us_cell_12
    us_cell_14
    us_cell_2
    us_cell_3
    us_cell_4
    us_cell_5
    us_cell_6
    us_cell_7
EXTRACT: jq -r '.CELL.ip_ranges[]'
```

- github-api (GitHub API addresses)

```
 SOURCE: https://api.github.com/meta 
EXTRACT: jq -r '.api[]'
```

- github-git (GitHub Git addresses)

```
 SOURCE: https://api.github.com/meta 
EXTRACT: jq -r '.git[]'
```
- github-web (GitHub Web addresses)

```
 SOURCE: https://api.github.com/meta 
EXTRACT: jq -r '.web[]'
```

The GUID value for below calls can be generated in via https://www.guidgenerator.com/ -- see http://aka.ms/ipurlws for more information.

- smtp.office365.com (Office365 SMTP addresses)

```
 SOURCE: https://endpoints.office.com/endpoints/worldwide?clientrequestid=GUID 
EXTRACT: jq -r '.[] | select(.urls[]? | contains("smtp.office365.com")) | .ips[]'
```

- *.mail.protection.outlook.com (Office365 SMTP addresses)

```
 SOURCE: https://endpoints.office.com/endpoints/worldwide?clientrequestid=GUID
EXTRACT: jq -r '.[] | select(.urls[]? | contains("*.mail.protection.outlook.com")) | .ips[]'
```

- gmail.com SPF (Google SMTP addresses)

```
 SOURCE: SPF (https://github.com/jschauma/spf/)
EXTRACT: spf -r 1.1.1.1 -j gmail.com | jq -r '.expanded[].pass?.total? | select( . != null ) | .ip4[]'
```
