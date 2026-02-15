# Bolt's Journal

## 2024-05-22 - Prompt Loading Overhead **Learning:** Static assets like prompt templates were being re-read and re-processed (regex for includes) on every agent execution. In a high-concurrency workflow with retries, this adds significant I/O overhead. **Action:** Implemented module-level caching for prompt templates. Always check for repetitive I/O operations on static resources.
