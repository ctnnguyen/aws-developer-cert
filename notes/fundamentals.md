# Fundamentals

## Encryption

### Approaches

- Encryption at rest
  - Designed to protect against physical theft and physical tampering
  - e.g. encrypted laptop (laptop encrypts data when writing data to internal storage, decrypts vice-versa)
  - Machine is useless to attacker without passcode
  - Generally used when one entity is involved
- Encryption in transit
  - Protects data while it's being transferred between two places
  - Data encrypted when data leaves machine
  - Decrypted by receiving party
  - Usually used when multiple identities or parties are involved

### Concepts

- Symmetric Encryption
  - Same secret key is used to encrypt and decrypt the ciphertext
  - Transportation of key is an issue (must do this in advance)
- Asymmetric Encryption
  - Public key used to encrypt data; private key used to decrypt data
  - Receiver needs to provide public key to sender
  - Generally used when 2+ parties are involved
- Signing
  - Encryption does not prove identity

## OSI Model

- Media layer is how data is transferred from point A to point B
- Host layer is how data is transformed into understandable format by both sides of a network connection

### Layer one - Physical

- Focuses on physical, shared medium
- Contains one broadcast and one collision network
- Defines standards that all devices will use to transmit and receive data
- Collision occurs when two devices try to transmit at the same time (corrupts data)
- No access control of the shared medium
- No uniquely, identifiable devices
- Everything is broadcast (cannot do device to device communication)

### Layer two - Data Link

- Device to device communication (identifiable devices)
- Provides controlled access to the shared medium (sharing)
- Collision detection
- Utilize switches (rather than hubs)

### Layer three - Network

- IP address (IPv4/v6) - cross network addressing (device to device communication)
- ARP - Find the MAC address for the IP
- Route - where to forward packets
- Route Tables - Multiple routes
- Router - moves packets from source to destination (encapsulating in layer 2 on the way)
- Only has one stream of communication - can't have different applications on devices communicating at same time

### Layer three - Transport

- TCP - used for reliability, ordering of data, error correction (e.g. HTTP, HTTPS, SSH)
- UDP - faster because no overhead, less reliable

## Hashing
- can only go one way
- cannot get original data from hash
- same data should always generate same hash
- collisions -> two different sets of data generates same hash
- md5 is not a secure algorithm like sha2-256
