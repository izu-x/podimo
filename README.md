<div align="center">

# Podimo to RSS

**Stream Podimo podcasts in any podcast app — no Podimo app required.**

Podimo is a proprietary podcast platform with exclusive shows behind a paywall. This tool bridges that gap by exposing your Podimo library as standard RSS feeds, compatible with any podcast client.

[![License: EUPL 1.2](https://img.shields.io/badge/License-EUPL_1.2-blue.svg)](https://joinup.ec.europa.eu/software/page/eupl)

</div>

---

## Table of Contents

- [Installation](#installation)
- [Docker](#docker)
- [Finding your Podcast ID](#finding-your-podcast-id)
- [Configuration](#configuration)
- [Bot Detection](#bot-detection)
- [Privacy](#privacy)
- [License](#license)
- [Support](#support)

---

## Installation

> Requires Python 3.8+

```sh
git clone https://github.com/izu-x/podimo
cd podimo
make update
make install
make start
```

Visit [http://localhost:12104](http://localhost:12104) — you should see the interface.

To make it accessible from other machines or adjust settings:

```sh
make config
```

A full list of options is in [.env.example](.env.example).

---

## Docker

```sh
docker run --rm \
    -e PODIMO_BIND_HOST=0.0.0.0:12104 \
    -p 12104:12104 \
    -v $(pwd)/cache:/src/cache \
    ghcr.io/thijsray/podimo:latest
```

Visit [http://localhost:12104](http://localhost:12104) once running.

See [.env.example](.env.example) for all available environment variables.

---

## Finding your Podcast ID

Each Podimo podcast has a unique UUID used to generate the RSS feed. The easiest way to find it:

1. Go to [open.podimo.com](https://open.podimo.com)
2. Search for and open the podcast page
3. Copy the UUID from the URL:

```text
https://open.podimo.com/podcast/09c55c96-9b1b-456e-bdf2-3abed3b61db5
                                 ^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^
                                 your Podcast ID
```

Use that ID when generating your feed URL in the interface.

---

## Configuration

All configuration is done via environment variables or the `.env` file. Run `make config` to edit it interactively.

Full reference: [.env.example](.env.example)

---

## Bot Detection

Depending on your usage patterns, Podimo may trigger anti-bot protections. You can route requests through a proxy service to work around this.

### Zenrows

1. Create a free account at [app.zenrows.com/register](https://app.zenrows.com/register)
2. Set the `ZENROWS_API` environment variable to your API key

### ScraperAPI

1. Create a free account at [dashboard.scraperapi.com/signup](https://dashboard.scraperapi.com/signup)
2. Set the `SCRAPER_API` environment variable to your API key

---

## Privacy

The tool handles credentials as follows:

- **Username and password** are used only to obtain an access token and are never written to disk
- **A cryptographic hash** of your credentials is kept in memory as a cache key
- **The Podimo access token** is cached in memory (or on disk if `STORE_TOKENS_ON_DISK=true`)

Nothing is ever logged.

---

## License

```text
Copyright 2022-2023 Thijs Raymakers

Licensed under the EUPL, Version 1.2 or – as soon they
will be approved by the European Commission - subsequent
versions of the EUPL (the "Licence");
You may not use this work except in compliance with the
Licence.

https://joinup.ec.europa.eu/software/page/eupl
```

---

## Support

If this tool saves you time, consider buying a coffee:

[![Buy Me A Coffee](https://www.buymeacoffee.com/assets/img/custom_images/orange_img.png)](https://www.buymeacoffee.com/thijsr) — original author

[![Buy Me A Coffee](https://www.buymeacoffee.com/assets/img/custom_images/orange_img.png)](https://buymeacoffee.com/izu_x) — fork maintainer
