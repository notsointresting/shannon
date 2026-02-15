# SENTINEL'S JOURNAL - CRITICAL LEARNINGS ONLY

## 2026-02-15 - Hardcoded Secrets in Configuration and Logs

**Vulnerability:** The pentest configuration file (`config.yaml`) required hardcoded secrets for authentication, which forced users to commit secrets or manually modify config files. Furthermore, these secrets were interpolated into prompt strings and logged to disk as part of the audit trail (prompt snapshots).

**Learning:** The configuration parser (`src/config-parser.ts`) did not support environment variable substitution, a standard practice for managing secrets. Consequently, the audit logger (`src/audit/logger.ts`) unknowingly persisted these secrets because the prompt content was fully resolved before logging.

**Prevention:**
1. Always implement environment variable substitution in configuration loaders to allow secrets to be injected from `.env` or the environment.
2. Ensure logging utilities (especially those logging raw inputs like prompts) have mechanisms to redact sensitive information before writing to persistent storage.
