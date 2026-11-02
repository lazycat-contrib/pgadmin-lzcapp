# pgAdmin 4 (LazyCat LPK)

PostgreSQL administration in the browser.

- Upstream: https://www.pgadmin.org/ (source: https://github.com/pgadmin-org/pgadmin4)
- Image: `dpage/pgadmin4:9.19.0` (Docker Hub, mirror mode, digest-matched)
- License: PostgreSQL licence (full text in `content/licenses/LICENSE`)
- Containers: single. pgAdmin is a client tool — it ships no database.

## Notes

- Port 80, user 5050, data dir `/var/lib/pgadmin`.
- Login seeded from `PGADMIN_DEFAULT_EMAIL` / `PGADMIN_DEFAULT_PASSWORD` deploy params.
- Behind the LazyCat https ingress the `PGADMIN_CONFIG_PROXY_X_*_COUNT` values matter — without
  them pgAdmin builds absolute URLs against the container's own http address. `X_PREFIX_COUNT=0`
  because the ingress serves the app at the root path.
- Session cookies marked Secure + SameSite=Lax, enhanced cookie protection on.
- `MASTER_PASSWORD_REQUIRED=False` so login does not need a second encryption passphrase.
- `PGADMIN_DISABLE_POSTFIX=True` — no mail service available.
- State persists on `/lzcapp/var/pgadmin`.
- Not yet verified on a real device.
