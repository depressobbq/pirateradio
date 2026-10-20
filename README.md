# 🏴‍☠️ Pirate Radio

> **The Unstoppable, Offline-First P2P Web Gateway**  
> *"Tune in, seed back, stay online."*

Pirate Radio is a transport-agnostic, censorship-resistant peer-to-peer network designed to make websites and media impossible to take down. By combining lightweight Proof-of-Work PNS (Pirate Name Service) metadata gossip with on-demand, pull-based block retrieval over an automated TCP mesh, Pirate Radio ensures that once a site is published, it lives on anywhere a node cares to cache and pin it.

---

## 🌟 Key Architecture Features

- **Pirate Name Service (PNS):** Decentralized handle claims verified via cryptographic keys and propagated automatically across active mesh peers without central DNS registrars.
- **Pull-Based Mesh Distribution:** Nodes exchange lightweight name claims rather than dumping bulk data globally. Content blocks are fetched on-demand by local node gateways only when requested.
- **Smart LRU & Permanent Pinning:** Configurable local SQLite storage (default 1 GB) automatically manages transient media via LRU eviction, while giving users interactive CLI tools (`pin` / `unpin`) to permanently anchor critical web assets against deletion.
- **Zero-Config Local Discovery:** Built-in UDP background beacons automatically discover adjacent local swarm nodes and sync active handle claims instantly.
- **Local Browser Gateway:** Every node runs an embedded Axum HTTP server (`http://localhost:8080/<handle>`), rendering decentralized HTML assets natively in any standard browser.
- **Sneakernet & Multi-Transport Support:** Pluggable adapters designed to support everything from TCP/IP mesh networks to physical file drops (`./radio_in` and `./site_in`).

---

## 🗂️ Workspace Crate Structure

Pirate Radio is organized as a modular Cargo workspace:

- `pirate-block/` — Content-addressing, BLAKE3/SHA hashing, and cryptographic signature verification.
- `pirate-identity/` — Key generation, persistent keypair recovery (`node_identity.key`), and node ID formatting.
- `pirate-pns/` — Proof-of-Work name claim generation, validation, and distributed registry.
- `pirate-storage/` — Local SQLite vault state store (`pirate_node_vault.db`), block persistence, and LRU eviction logic.
- `pirate-sync/` — Vector clocks, conflict-free state tracking, and DHT bridge routing.
- `pirate-transport/` — TCP transport adapter, background UDP auto-discovery beacons, and physical file scanners.
- `pirate-integrations/` — Core integration hooks and cross-module utilities.
- `pirate-radio` (Binary Root) — Axum web gateway, interactive CLI management console, and file watchers.

---

## 🚀 Quickstart Guide

### 1. Build the Workspace
Ensure you have Rust and Cargo installed, then compile the project:
```bash
cargo build --release
```

### 2. Launch Primary Node
Run your first node. It will automatically generate an identity keypair, bind an available TCP transport port (e.g., `9001`), and spin up a local web gateway (e.g., `http://127.0.0.1:8080`).
```bash
cargo run
```

### 3. Publish a Website
Drop any standard HTML, CSS, or JS file into the `./site_in/` directory:
```bash
echo "<h1>Sovereign P2P Web Active</h1>" > ./site_in/index.html
```
The node will automatically ingest the asset into its local vault, link it to your node's PNS handle, and broadcast the claim announcement to the mesh.

### 4. Connect a Secondary Node & Browse
In a separate terminal, launch a second node:
```bash
cargo run
```
It will automatically discover the first node via local UDP/TCP discovery, sync the PNS handle claim, and allow you to view the site through its own gateway port (`http://127.0.0.1:8081/<your-handle>`). When requested, the secondary node pulls the content block on-demand over the mesh and caches it locally.

### 5. Interactive CLI Commands
Type `help` inside your node terminal to view available management actions:
- `status` — Display your active node handle and cryptographic ID.
- `pin <handle>` — Permanently lock a site's content block into your local vault, making it immune to LRU cache eviction.
- `unpin <handle>` — Return a pinned site block to standard LRU management.
- `exit` / `quit` — Gracefully shut down the node.

---

## Contributing

We welcome contributions from anyone who believes in a free, grass-roots, and resilient internet. Please check out [CONTRIBUTING.md](CONTRIBUTING.md) to get started.

## License

Distributed under the [GNU General Public License v3.0](LICENSE).
