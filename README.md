<h1 align="center">devyce</h1>
<p align="center">Open source platform for deploying static sites and frontend applications.</p>
<p align="center">
<a href="https://twitter.com/CybersafeLabs">Twitter</a>
</p>

## Disclaimer

devyce is in active development. Also after release you will need to install devyce on a VPS Server of your own, after which an official devyce installation will be deployed to an VPS Server.
Please note that the domain `devyce.site` does not exist yet please replace devyce.site to your own domain name thank you.

![Meli demo screenshot](https://raw.githubusercontent.com/getmeli/meli-brand/latest/screens/meli-site-branch.png)

## Getting started

Want to change the way you ship front-end, forever ? Let's get started !

Install devyce first.
1. After you have installed devyce and have successfully logged in:
    1. Create a site in your dashboard, say `my-site`
    1. [Upload a release with the `@getmeli/meli` CLI](https://docs.meli.sh/get-started/upload-a-site-to-meli)
    1. Setup `my-domain.com` to point to your devyce server at `my-site.devcye.site`

## Features

- Deploy unlimited static sites under a primary domain
- Unlimited organizations, teams, users and sites
- Seamless custom domains redirection
- [Many ways to authenticate](https://docs.meli.sh/authentication)
- [Automatic HTTPs certificate issuing with letsencrypt (or private ACME server)](https://docs.meli.sh/configuration/ssl)
- [Deploy branches](https://docs.meli.sh/get-started/branches)
- [API with per-endpoint scopes](https://docs.meli.sh/api/get-started)
- Integrations ([Webhooks](https://docs.meli.sh/integrations/webhooks), [Slack](https://docs.meli.sh/integrations/slack), [Mattermost](https://docs.meli.sh/integrations/mattermost), [Email](https://docs.meli.sh/integrations/email))
- Easily [deploy](https://docs.meli.sh/get-started/installation#installation) and [upgrade](https://docs.meli.sh/get-started/upgrade-and-downgrade) with Docker Compose
- [Password protected pages](https://docs.meli.sh/branches/password-protected-pages)
- [Path overrides with in-memory files or reverse proxies](https://docs.meli.sh/branches/redirects#redirects)
- [Single page application mode](https://docs.meli.sh/get-started/single-page-applications-spa)
- Get deploy URL in pull requests and commit status
- [Heavily customizable](https://docs.meli.sh/environment-reference/server)
- [ ] Increase test coverage
- [ ] API documentation
- [ ] Documentation
- [ ] Build an official project website
- [ ] Create a community discussion branch
- [ ] Deploy a cloud version
- [ ] Translations
- [ ] Extend integrations
- [ ] Accessibility

## Development

### Start UI

1. Clone the [UI repo](https://github.com/CyberSafe-Labs/devyce-ui).
1. `npm i && npm start`
1. The app is accessible from http://localhost:3001, but we develop from http://localhost:8080 (see below)

### Start Caddy and the API

1. Run `docker-compose -f ./docker-compose-dev.yml up -d`
1. Configure your `.env` (copy `.env.example` to start with)
1. Run `npm i && npm start`

If you develop with the UI, you'll need to clone the [UI repo](https://github.com/getmeli/meli-ui), then start it.

You can now browse at `http://localhost:8080`:
- `http://localhost:8080/` => UI
- `http://localhost:8080/api`, `http://localhost:8080/auth` and `http://localhost:8080/socket.io` => API
- `http://devyce.site` => your sites will be served here

### DNS config

You need to configure your machine to allow wildcard domains for development. We've got a few ways to do this.

#### Use devyce.site

We've configured devyce.site to point to 127.0.0.1, so you can develop with it. Update your `.env`.

```
MELI_SITES_URL=devyce.site
```

Your sites will be served at `*.devyce.site`.

Pros: simple, no config required
Cons: you need to be connected to the internet

#### Using /etc/hosts

Unfortunately, /etc/hosts doesn't support wildcard domains, so you'll need to edit /etc/hosts for every site added to devyce:

```
127.0.0.1 my-site.test
127.0.0.1 my-channel.my-site.test
```

Pros: simple, can develop without internet
Cons: have to reconfigure every time you add a site

#### Using dnsmasq

```
brew install dnsmasq

# tell dsnmasq to point *.test to 127.0.0.1
echo "address=/test/127.0.0.1" > /usr/local/etc/dnsmasq.conf

# start daemon
brew services start dnsmasq

# make OSX point to dnsmasq
sudo mkdir -p /etc/resolver

# tell os x to point *.test to 127.0.0.1
sudo echo "nameserver 127.0.0.1" > /etc/resolver/test

ping hello.test
```

Your sites will be served at `*.test`.

Pros: you don't need to be connected to the internet, no need to reconfigure /etc/hosts
Cons: a bit complex, config required

## License

CSL Non-Commercial License
