# Security

GreenNode AI Gateway ensures the protection of sensitive customer information such as authentication tokens and API keys through the following mechanisms:

1. **User Authentication Token**
   * Displayed only once at the time of creation.
   * Encrypted and securely stored.
   * Can be deleted at any time when no longer in use.
2. **API Key for Calling LLM Models**
   * Customer-provided API keys are encrypted before being stored.
   * Can be updated or deleted whenever needed.
