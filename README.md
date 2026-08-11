Ansible Role: Karakeep-docker
=============================

Install Karakeep (formerly Hoarder) Docker Compose project.

- https://karakeep.app/
- https://github.com/karakeep-app/karakeep

Requirements
------------

Requires the following to be installed:
- docker
- docker compose

Role Variables
--------------

Common Docker projects variables:

```yaml
# Base directory for Docker projects
docker_projects_path: # /var/apps
```

Available role variables are listed below, along with default values (see `defaults/main.yml`):

```yaml
# Docker project variables

karakeep_project_name: karakeep

# Docker project dynamic vars (uses `docker_project_name` prefix, adapt if overridden)

karakeep_traefik_loadbalancer_server_port: 3000

# Main service additional docker-compose options (ex: cpu_shares, deploy, ...)
karakeep_service_additional_options: |
  #ports:
  #  - 3000:3000
```

```yaml
# Karakeep project variables

# ghcr.io/karakeep-app/karakeep image version
karakeep_docker_version: release

# ghcr.io/karakeep-app/karakeep-chrome image version
karakeep_chrome_version: release

# getmeili/meilisearch image version
karakeep_meilisearch_version: v1.41.0
```

```yaml
# Application logging verbosity level
karakeep_log_level: debug

# Workers
karakeep_workers_port: 0
karakeep_workers_host: 127.0.0.1
karakeep_workers_enabled_workers:
karakeep_workers_disabled_workers:

# The path where crawled assets will be stored. If not set, defaults to `${DATA_DIR}/assets`
karakeep_assets_dir:

# Public address of service
karakeep_nextauth_url: http://localhost:3000

# Random string used to sign the JWT tokens. Generate one with `openssl rand -base64 36`
karakeep_nextauth_secret: super_random_string
# Master key configured for meilisearch
karakeep_meili_master_key: another_random_string

# Sets the maximum allowed asset size (in MB) to be uploaded
karakeep_max_asset_size_mb: 50
# If set to true, latest release check will be disabled in the admin panel.
karakeep_disable_new_release_check: false
# If set to true, API rate limiting will be enabled.
karakeep_rate_limiting_enabled: false
# Time window (ms) for per-domain crawler rate limiting
karakeep_crawler_domain_rate_limit_window_ms:
# Maximum crawler requests allowed per domain inside the configured window
karakeep_crawler_domain_rate_limit_max_requests:
# Enables WAL mode for the sqlite database. This should improve the performance of the database.
karakeep_db_wal_mode: false
# Number of concurrent workers for search indexing tasks
karakeep_search_num_workers: 1
# How long to wait for a search indexing job to finish before timing out
karakeep_search_job_timeout_sec: 30
# Number of concurrent workers for webhook delivery
karakeep_webhook_num_workers: 1
# Number of concurrent workers for asset preprocessing tasks (image processing, OCR, etc.)
karakeep_asset_preprocessing_num_workers: 1
# How long to wait for an asset preprocessing job to finish before timing out
karakeep_asset_preprocessing_job_timeout_sec: 60
# Number of concurrent workers for rule engine processing
karakeep_rule_engine_num_workers: 1
# The maximum number of RSS feeds a user can create
karakeep_max_rss_feeds_per_user: 1000
# The maximum number of webhooks a user can create
karakeep_max_webhooks_per_user: 100
```

```yaml
# Asset Storage (S3-compatible object storage). Setting karakeep_asset_store_s3_endpoint enables S3 storage.
karakeep_asset_store_s3_endpoint:
karakeep_asset_store_s3_region:
karakeep_asset_store_s3_bucket:
karakeep_asset_store_s3_access_key_id:
karakeep_asset_store_s3_secret_access_key:
karakeep_asset_store_s3_force_path_style: false
```

```yaml
# Authentication / Signup

# If enabled, no new signups will be allowed and the signup button will be disabled in the UI
karakeep_disable_signups: false
# If enabled, only signups and logins using OAuth are allowed and the signup button and login form for local accounts will be disabled in the UI
karakeep_disable_password_auth: false
# Whether email verification is required during signup. Requires SMTP to be configured.
karakeep_email_verification_required: false
# Auto-redirect to the OAuth provider on the login page
karakeep_oauth_auto_redirect: false
# The "wellknown Url" for openid-configuration as provided by the OAuth provider
karakeep_oauth_wellknown_url:
# The "Client Secret" as provided by the OAuth provider
karakeep_oauth_client_secret:
# The "Client ID" as provided by the OAuth provider
karakeep_oauth_client_id:
# Expected JWS signing algorithm for OIDC ID tokens, if your provider doesn't use the default
karakeep_oauth_id_token_signed_response_alg:
# Full list of scopes to request (space delimited)
karakeep_oauth_scope: "openid email profile"
# The name of your provider. Will be shown on the signup page as "Sign in with <name>"
karakeep_oauth_provider_name: "Custom Provider"
# Whether existing accounts in Karakeep stored in the database should automatically be linked with your OAuth account.
karakeep_oauth_allow_dangerous_email_account_linking: false
# How long to wait for a response from the OAuth provider (ms)
karakeep_oauth_timeout: 3500
```

```yaml
# Inference Configs (For automatic tagging)
karakeep_openai_api_key:
karakeep_openai_base_url:
karakeep_openai_proxy_url:
karakeep_openai_timeout_sec:
karakeep_openai_service_tier:
karakeep_openai_reasoning_effort:
karakeep_ollama_base_url:
karakeep_ollama_keep_alive:
karakeep_semantic_search_enabled: true
karakeep_inference_text_model: gpt-5.6-luna
karakeep_inference_image_model: gpt-4o-mini
karakeep_embedding_enable_auto_indexing:
karakeep_embedding_openai_api_key:
karakeep_embedding_openai_base_url:
karakeep_embedding_text_model: text-embedding-3-small
karakeep_embedding_text_model_dimension_override:
karakeep_embedding_context_length: 8000
karakeep_embedding_dimensions: 1536
karakeep_embedding_num_workers: 1
karakeep_embedding_job_timeout_sec: 60
karakeep_inference_context_length: 2048
karakeep_inference_max_output_tokens: 2048
karakeep_inference_use_max_completion_tokens: true
karakeep_inference_lang: english
karakeep_inference_num_workers: 1
karakeep_inference_enable_auto_tagging: true
karakeep_inference_enable_auto_summarization: false
karakeep_inference_job_timeout_sec: 30
karakeep_inference_fetch_timeout_sec: 300
karakeep_inference_output_schema: structured
```

```yaml
# Crawler Configs
karakeep_crawler_num_workers: 1
karakeep_browser_web_url:
karakeep_browser_websocket_url:
karakeep_browser_connect_ondemand: false
karakeep_crawler_download_banner_image: true
karakeep_crawler_store_screenshot: true
karakeep_crawler_full_page_screenshot: false
karakeep_crawler_screenshot_timeout_sec: 5
karakeep_crawler_store_pdf: false
karakeep_crawler_full_page_archive: false
karakeep_crawler_job_timeout_sec: 60
karakeep_crawler_navigate_timeout_sec: 30
karakeep_crawler_preflight_user_agent:
karakeep_crawler_parse_timeout_sec: 60
karakeep_crawler_parser_mem_limit_mb: 512
karakeep_crawler_video_download: false
karakeep_crawler_video_download_max_size: 50
karakeep_crawler_video_download_timeout_sec: 600
karakeep_crawler_enable_adblocker: true
karakeep_crawler_enable_autoconsent: true
karakeep_crawler_ytdlp_args:
karakeep_crawler_monolith_timeout_sec: 5
karakeep_crawler_monolith_args:
karakeep_browser_cookie_path:
karakeep_html_content_size_inline_threshold_bytes: 5120
```

```yaml
# OCR Configs
karakeep_ocr_cache_dir: /tmp
karakeep_ocr_langs: eng
karakeep_ocr_confidence_threshold: 50
karakeep_ocr_use_llm: false
```

```yaml
# Webhook Configs
karakeep_webhook_timeout_sec: 5
karakeep_webhook_retry_times: 3
```

```yaml
# SMTP Configuration
karakeep_smtp_host:
karakeep_smtp_port: 587
karakeep_smtp_secure: false
karakeep_smtp_user:
karakeep_smtp_password:
karakeep_smtp_from:
```

```yaml
# Proxy Configuration
karakeep_crawler_http_proxy:
karakeep_crawler_https_proxy:
karakeep_crawler_no_proxy:
karakeep_crawler_allowed_internal_hostnames:
```

```yaml
# Monitoring
karakeep_otel_tracing_enabled: false
karakeep_otel_exporter_otlp_traces_endpoint:
karakeep_otel_service_name: karakeep
karakeep_otel_sample_rate: 1.0
karakeep_event_logs_enabled: false
karakeep_otel_event_logs_export_enabled: false
karakeep_otel_exporter_otlp_logs_endpoint:
karakeep_prometheus_auth_token:
```

Dependencies
------------

This role depends on :
- [djuuu.docker_project](https://github.com/Djuuu/ansible-role-docker-project)

Some variables allow integration with:
- [djuuu.traefik_docker](https://github.com/Djuuu/ansible-role-traefik-docker)

Example Playbook
----------------

```yaml
- hosts: all
  gather_facts: false

  roles:
    - djuuu.karakeep_docker
```

License
-------

Beerware License
