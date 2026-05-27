# ZAP Protocol — Papers

> **Docs:** [ZAP design papers](https://zap-proto.dev/docs) · part of the [ZAP Protocol](https://zap-proto.io)


Formal results on the ZAP wire, transport, and sub-protocol family. Every paper is in LaTeX, brand-neutral, and accompanies a proof in [`../proofs/`](../proofs/).

| # | Paper | Topic | Key result |
|---|---|---|---|
| 1 | [pq-hybrid-kem](./pq-hybrid-kem/main.tex) | Z-Wing triple-hybrid KEM (X25519 + ML-KEM-768 + ML-KEM-1024) | IND-CCA2-AKE bound 2^-87 under standard assumptions |
| 2 | [zero-copy-throughput](./zero-copy-throughput/main.tex) | Throughput vs gRPC/HTTP-2/QUIC/JSON | p99 9–14× small msg vs JSON; 3.5–6× vs gRPC |
| 3 | [transport-vs-jwt](./transport-vs-jwt/main.tex) | Transport-layer mutual auth vs bearer JWT | ZAP advantage strictly dominates JWT; mint-storm impossibility |
| 4 | [rns-identity-binding](./rns-identity-binding/main.tex) | KEM-bound service naming | Spoofing reduces to KEM key compromise + sig forge + small audit-able root |
| 5 | [streaming-tail-latency](./streaming-tail-latency/main.tex) | Multi-stream pubsub, FEC, no head-of-line blocking | Per-stream latency conditionally independent of other streams |
| 6 | [fix-trading-channel](./fix-trading-channel/main.tex) | FIX 4.4/5.0 over ZAP | 1.5–8μs/msg savings vs FIX-over-TLS, 30–50% wire bytes |
| 7 | [agent-communication](./agent-communication/main.tex) | ZAP-MCP / ZAP-A2A non-repudiation | Audit artifact = signed frame; provenance chain bound k·(EUF-CMA + q²/2^257) |
| 8 | [composability](./composability/main.tex) | Categorical composition of sub-protocols | ZAP-base is initial; tight-embedding additive loss bound |

## What composes onto what

Per the composability paper, every sub-protocol is a tight embedding of ZAP-base. Properties chain:

```
        ZAP-base  (PQ conf, mutual auth, zero-copy)
         ↑
         ├── zap-http          (HTTP req/resp; inherits all ZAP-base)
         ├── zap-ws            (multi-stream pubsub + FEC; HOL-blocking elimination)
         ├── zap-rns           (KEM-bound naming; inherits ZAP-base + adds spoofing reduction)
         ├── zap-fix           (FIX semantics; tail-latency-bounded)
         ├── zap-mcp           (MCP non-repudiation per frame)
         ├── zap-acp           (FIPA-style speech acts, signed)
         └── zap-a2a           (Google Agent2Agent, audit-grade)
```

A `zap-fix` session over `zap-rns` over `zap-ws` over `zap-base` inherits `zap-base`'s post-quantum guarantees automatically — no FIX-specific PQ proof needed.

## Build

Each paper directory has a `Makefile`. Most build under `pdflatex` (TeX Live 2025); a few are tested with `tectonic`. Compiled PDFs are checked in where the toolchain was available locally.

```sh
cd pq-hybrid-kem && make    # produces main.pdf
cd ../proofs/pq-hybrid-kem && make    # produces proof.pdf
```

## License

CC-BY-4.0 for the paper text; MIT OR Apache-2.0 for any code samples.