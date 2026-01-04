# Storage Design

## Current State
- 1TB HDD used for application and media data
- No redundancy (single-disk)

## Risk Management
- Regular backups of critical data
- Media considered non-critical

## Future Plan
- Add second disk
- Migrate to ZFS mirror for redundancy
- Separate pools for critical data vs media
