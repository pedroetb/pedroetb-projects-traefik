# traefik

Modern reverse proxy and load balancer with automatic and dynamic configuration

## Set DNS challenge using OVH as DNS provider

> Extracted from:
>
> - <https://blog.ichasco.com/traefik-configurar-dns-01-challenges-de-lets-encrypt-en-ovh-con-wildcards/>
> - <https://go-acme.github.io/lego/dns/ovh/index.html>

First, you need to create a new app at OVH from <https://eu.api.ovh.com/createApp/>.

This will provide your values for `OVH_APPLICATION_KEY` and `OVH_APPLICATION_SECRET`.

Then, use the values of `OVH_APPLICATION_KEY` and `TRAEFIK_DOMAIN` (your main domain) replaced at following command:

```sh
curl \
  -XPOST \
  -H "X-Ovh-Application: ${OVH_APPLICATION_KEY}" \
  -H "Content-type: application/json" \
  https://eu.api.ovh.com/1.0/auth/credential \
  -d '{
    "accessRules": [{
      "method": "GET",
      "path": "/*"
    },{
      "method": "POST",
      "path": "/*"
    },{
      "method": "PUT",
      "path": "/*"
    },{
      "method": "DELETE",
      "path": "/*"
    }],
    "redirection": "${TRAEFIK_DOMAIN}/"
  }'
```

This will provide a response containing `OVH_CONSUMER_KEY` and a URL to grant required permissions. Enter to URL and set `Unlimited` for validity.

## References

- Check `traefik` repository at <https://github.com/traefik/traefik>.
- Check official docs at <https://doc.traefik.io/traefik/>.
