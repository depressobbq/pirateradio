# 🏴‍☠️ Pirate Radio

> **The Unstoppable, Offline-First P2P Web Protocol**  
> *"Tune in, seed back, stay online."*

Pirate Radio is a transport-agnostic, delay-tolerant peer-to-peer network designed to make websites and media impossible to censor or permanently take down. As long as a single copy of a file exists on a local hard drive, a USB flash drive, or a low-power radio link, it can be served, verified, and re-seeded into the global mesh.

---

## Key Features

* **`pirate://` Cryptographic Addressing:** Sites are identified by public key pairs, using signed append-only Merkle DAGs for updates rather than fragile static hashes.
* **Transport-Agnostic Engine:** Operates seamlessly across TCP/IP, ad-hoc local Wi-Fi, Bluetooth LE, audio voice modems, and physical USB "Sneakernet" bundles.
* **Offline-First "BBS" Spooling:** Browse, post, and update content offline. Outgoing actions queue into a local spool and sync automatically when any connection is made.
* **Smart LRU & Pinning Cache:** Configurable local storage limits auto-evict least-recently-used transient media while allowing users to permanently pin media.
* **Version Timelines:** Historical revisions are preserved side-by-side using content-addressable blocks, allowing "lost media" to be restored without corrupting new states.

---

## Repository Structure

* `src/block/` — Content-addressing, hashing (BLAKE3), and cryptographic signature verification.
* `src/storage/` — Local SQLite state store, chunk compression, and LRU cache manager.
* `src/transport/` — Pluggable transport adapter interface (Sockets, USB Auto-Ingress, Audio Modems).
* `src/sync/` — Outbound message spooler and CRDT conflict-free merge engine.

---

## Contributing

We welcome contributions from anyone who believes in a free, grass-roots, and resilient internet. Please check out [CONTRIBUTING.md](CONTRIBUTING.md) to get started.

## License

Distributed under the [GNU General Public License v3.0](LICENSE).
