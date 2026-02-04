# Changelog
All notable changes to this project will be documented in this file.

The format is based on [Keep a Changelog](https://keepachangelog.com/en/1.0.0/),
and this project adheres to [Semantic Versioning](https://semver.org/spec/v2.0.0.html).

## [4.1.0] - 2026-02-03
### Security
- **SECURITY**: OAuth2 credentials now stored as encrypted system preferences
  - Credentials encrypted using AES-256 via Koha::Encryption module
  - Client secret masked in admin interface
  - Eliminates plain-text credential storage in configuration files

### Added
- New `get_oauth_credentials()` method with fallback from system preference to koha-conf.xml
- New `encrypt_credentials()` and `decrypt_credentials()` helper methods
- New `migrate_credentials_from_koha_conf()` method for automatic credential migration
- New credential display methods: `get_display_auth_url()`, `get_display_client_id()`, `get_display_notice_url()`, `get_display_customer_id()`
- New `has_oauth_credentials()` method to check credential configuration status
- New `set_encrypted_syspref()` method for storing encrypted credentials

### Changed
- Updated `configure()` to support encrypted credential input form
- Updated `get_oauth_token()` to use new credential retrieval methods
- Updated `send_to_webhook()` to use new credential retrieval methods
- Updated `install()` to automatically migrate credentials from koha-conf.xml
- Updated `upgrade()` to support credential migration on plugin upgrades
- Updated documentation to reflect new credential storage approach

### Compatibility
- Maintains full backward compatibility with existing koha-conf.xml configuration
- Automatic migration ensures smooth transition to encrypted system preferences
- Both configuration methods (system preference and koha-conf.xml) can coexist

## [4.0.0] - 2024-12-03
### Changed
- **BREAKING**: Renamed plugin from MessageBee to WebhookNotifications
- **BREAKING**: Replaced SFTP upload with HTTP webhook (OAuth2 + REST API)
- **BREAKING**: Changed YAML trigger from `messagebee: yes` to `webhook: yes`
- **BREAKING**: Renamed all environment variables from `MESSAGEBEE_*` to `WEBHOOK_*`
- Renamed API namespace from `/messagebee/` to `/webhook_notifications/`

### Added
- OAuth2 client credentials authentication flow
- Configurable payload format (full enriched data or minimal IDs only)
- Support for optional `customer-id` header via `WEBHOOK_CUSTOMER_ID` env var

### Removed
- SFTP upload functionality (replaced with HTTP POST)
- `Net::SFTP::Foreign` dependency

## [3.1.0] - 2022-05-19
- Add patron/account_balance to the JSON data
- Wrap most logic in try/catch to keep crashes from allowing messagebee yaml to be emailed by Koha

## [3.0.0] - 2022-05-19
- Update JSON data structure

## [0.0.1] - 2021-06-30
### Added
- Initial commit!
