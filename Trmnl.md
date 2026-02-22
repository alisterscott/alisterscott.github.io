---
title:  TRMNL Plugins
---

## Background

I am a big fan of [TRMNL](https://trmnl.com/) e-ink devices:

> TRMNL is an e-ink companion that helps you stay focused.

I have authored a number of open-source plugins for these devices:

1. [TRMNL Brisbane Bin Collection Calendar](https://github.com/alisterscott/trmnl-bne-bin)
2. [TRMNL International Flip Date Clock](https://github.com/alisterscott/trmnl-flip-date)
3. [TRMNL Simplenote](https://github.com/alisterscott/trmnl-simplenote)
4. [TRMNL Translink](https://github.com/alisterscott/trmnl-translink)

## Running `trmnlp` on a Github Codespaces instance

It's possible to run the [`trmnlp`](https://github.com/usetrmnl/trmnlp) development environment on a Github Codespaces instance with a few small tweaks:

In your `.devcontainer/devcontainer.json` make sure you have ruby installed (I use the Playwright docker image so I can run Playwright tests against my plugin screens, more on this below), and forward port 4567 for the trmnlp preview front end.

```json
{
  "image": "mcr.microsoft.com/playwright:v1.58.0",
  "forwardPorts": [6080, 4567],
  "postCreateCommand": "rbenv local && bundler install && npm install",
  "features": {
    "desktop-lite": {
      "webPort": "6080"
    },
    "ghcr.io/devcontainers/features/ruby:1": {},
    "git-lfs": "latest"
  }
}
```

I add a `Gemfile` and 

```
source 'https://rubygems.org'

gem 'trmnl_preview', '0.7.1'
```

Once this is set up you can use rbenv to set your ruby version (I use v3.4.8), run `bundler install` to install `trmnlp` and finally you can run:

`APP_ENV=production trmnlp serve` to start `trmnlp` which runs on port 4567 forwarded above.

Note the `APP_ENV=production` environment variable is required to allow the port forwarding on Codespaces to work and be accessible via an external address.
