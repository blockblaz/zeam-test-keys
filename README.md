# zeam-test-keys

Pre-generated XMSS validator key pairs for zeam CI and testing.

## Contents

- 32 validator key pairs (index 0-31)
- Generated with deterministic seeds (`test_validator_{i}`)
- 1000 active epochs per key
- ~8MB per private key (SSZ-encoded), 52 bytes per public key

## Usage

Added as a git submodule in zeam:

```bash
git submodule update --init test-keys
```

Keys are loaded by `getTestKeyManager()` in `pkgs/key-manager/src/lib.zig` instead of generating at runtime.

## Regenerating

```bash
cd zeam
zig build tools
./zig-out/bin/zeam-tools keygen --num-validators 32 --num-active-epochs 1000 --output-dir test-keys
```

## Format

```
hash-sig-keys/
├── validator_0_sk.ssz   # Private key (SSZ, ~8MB)
├── validator_0_pk.ssz   # Public key (SSZ, 52 bytes)
├── ...
└── validator_31_pk.ssz
validator-keys-manifest.yaml  # Metadata + pubkey hex
```
