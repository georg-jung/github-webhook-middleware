# GitHub Webbhook Middleware

GitHub Webhook Middleware is a middleware plugin for [Traefik](https://github.com/containous/traefik) which validates the signature in the [`X-Hub-Signature-256` header](https://docs.github.com/en/developers/webhooks-and-events/webhooks/securing-your-webhooks).

## Configuration

Start with command

```yaml
command:
  - "--experimental.plugins.gh-webhook-middleware.modulename=github.com/23deg/jwt-middleware"
  - "--experimental.plugins.gh-webhook-middleware.version=v0.1.2"
```

Activate plugin in your config  

```yaml
http:
  middlewares:
    my-gh-webhook-middleware:
      plugin:
        gh-webhook-middleware:
          secret: SECRET
          authHeader: X-Hub-Signature-256
          headerPrefix: sha256=
```

Use as docker-compose label  

```yaml
  labels:
        - "traefik.http.routers.my-service.middlewares=my-gh-webhook-middleware@file"
```

> Inspired by [23deg/jwt-middleware](https://github.com/23deg/jwt-middleware)
