# showroom-troshka-sno-base

A stub [Showroom](https://github.com/rhpds/showroom) lab guide for a base
**Single Node OpenShift (SNO)** environment provisioned by
[Troshka](https://github.com/rhpds/troshka).

## Use with Troshka

Point a showroom container's **Content repo** at this repository (and set the
**Content ref**) with *Build content at deploy* enabled. Troshka clones this
repo into the showroom pod, injects its generated `ui-config.yml`, and builds
the Antora site with the nookbag UI.

## Layout

```
site.yml                              # Antora playbook (must be named site.yml, at repo root)
content/
  antora.yml                          # component descriptor — name MUST be "modules"
  modules/ROOT/
    nav.adoc                          # left-nav
    pages/
      index.adoc                      # overview
      01-bastion.adoc                 # Bastion Terminal tab
      02-console.adoc                 # OCP Console (web-proxy tab)
      03-verify-sno.adoc              # verify the single-node cluster
```

## Notes

- **Do not** add `ui-config.yml` or `nginx.conf` — Troshka generates and
  injects both into the showroom pod at deploy.
- The component `name:` in `content/antora.yml` **must remain `modules`** to
  match Troshka's generated `ui-config.yml`; any other name renders a blank
  right panel.
- The playbook **must** be named `site.yml` at the repo root — Troshka's Antora
  builder runs with `ANTORA_PLAYBOOK=site.yml`.

## Build locally (optional)

```sh
npx antora --fetch site.yml
# built site: ./www/www
```
