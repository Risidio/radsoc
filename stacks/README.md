# risidio stacks

## Stacks Node Test Net

[Run a Stacks Testnet Node](https://docs.blockstack.org/core/smart/neon-node.html).

```
docker volume create stacks-vol
```


```
FROM rust:latest as build

WORKDIR /src/stacks-blockchain

COPY . .

RUN cd testnet && cargo install --path . --root .

FROM debian:stable-slim
RUN apt-get update && apt-get install -y --no-install-recommends libssl-dev
COPY --from=build /src/stacks-blockchain/testnet/bin /bin

CMD ["stacks-node", "neon"]
```
