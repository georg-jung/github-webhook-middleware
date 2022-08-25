# GitHub Webhook Middleware

GitHub Webhook Middleware is a middleware plugin for [Traefik](https://github.com/containous/traefik) which validates the signature in the [`X-Hub-Signature-256` header](https://docs.github.com/en/developers/webhooks-and-events/webhooks/securing-your-webhooks).

## Configuration

Install with command

```yaml
command:
  - "--experimental.plugins.gh-webhook.modulename=github.com/georg-jung/github-webhook-middleware"
  - "--experimental.plugins.gh-webhook.version=v0.1.2"
```

Or install inside static config file:

```yaml
experimental:
  plugins:
    gh-webhook:
      modulename: github.com/georg-jung/github-webhook-middleware
      version: v0.1.2
```

Activate plugin in your dynamic config file

```yaml
http:
  middlewares:
    my-gh-webhook-middleware:
      plugin:
        gh-webhook:
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
