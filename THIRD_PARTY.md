# Third-party inventory

The local pilot runs Keila from an unmodified, pinned upstream source commit. Arkova's Dockerfile follows Keila's upstream `ops/Dockerfile`, changing only build-context paths and pinning the two official Elixir base-image digests.

| Component | Version | Pin | License | Source |
| --- | --- | --- | --- | --- |
| Keila | 0.30.2 | Git commit `6fa09dce28e2a67dcfc14c5526588b53477ba9ed` | AGPL-3.0 | <https://github.com/pentacent/keila/tree/v0.30.2> |
| Elixir build image | 1.18 Alpine | OCI index `sha256:caa6412c072c4b11e8c6798108388702c2791b4f8bad41e42c27ea5be881e2dc` | Apache-2.0 plus bundled components | <https://hub.docker.com/_/elixir> |
| Elixir runtime image | 1.18 / OTP 27 Alpine | OCI index `sha256:34260a722c6a6fa659aad9dd09e73466f5692a899e7edb60d43b0d51d4738c4f` | Apache-2.0 plus bundled components | <https://hub.docker.com/_/elixir> |
| PostgreSQL | 17.11 Alpine | OCI index `sha256:18cfe3ef5e6815560c98237d6216d1e5119702fb0f3894c8785dd58b8bbe5d73` | PostgreSQL License | <https://github.com/docker-library/postgres> |
| Mailpit | 1.30.7 | OCI index `sha256:d5ecbb067db3705fa953d79e1b7f81ef84038df67aba6c52825d8c02a1ea748a` | MIT | <https://github.com/axllent/mailpit/tree/v1.30.7> |

Keila's AGPL-3.0 obligations remain with Keila. This pilot does not modify Keila or combine Arkova proprietary code into it.
